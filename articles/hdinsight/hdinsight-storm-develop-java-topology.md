---
title: "Пример топологии Java для Apache Storm в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как создать топологии Apache Storm на языке Java с помощью создания примера топологии подсчета слов."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm, пример apache storm, storm java, пример топологии storm"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="a1328-104">Создание топологии Apache Storm на языке Java</span><span class="sxs-lookup"><span data-stu-id="a1328-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="a1328-105">Узнайте, как создать топологию на основе Java для Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="a1328-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="a1328-106">Вы создадите топологию Storm, реализующую приложение подсчета слов.</span><span class="sxs-lookup"><span data-stu-id="a1328-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="a1328-107">Чтобы собрать и упаковать проект, вы будете использовать Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="a1328-108">Затем вы узнаете, как определить топологию с помощью платформы Flux.</span><span class="sxs-lookup"><span data-stu-id="a1328-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-109">Платформа Flux доступна в Storm 0.10.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a1328-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="a1328-110">Storm 0.10.0 доступна в HDInsight 3.3 и 3.4.</span><span class="sxs-lookup"><span data-stu-id="a1328-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="a1328-111">После выполнения действий, описанных в этом документе, вы сможете развернуть топологию в Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1328-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-112">Полная версия примеров топологий Storm, созданных в рамках этого руководства, доступна здесь: [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="a1328-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1328-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1328-113">Prerequisites</span></span>

* [<span data-ttu-id="a1328-114">Java Developer Kit (JDK) версии 7</span><span class="sxs-lookup"><span data-stu-id="a1328-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="a1328-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): система сборки проектов для Java.</span><span class="sxs-lookup"><span data-stu-id="a1328-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="a1328-116">Текстовый редактор или интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="a1328-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="a1328-117">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="a1328-117">Configure environment variables</span></span>

<span data-ttu-id="a1328-118">Во время установки Java и JDK могут быть установлены следующие переменные среды.</span><span class="sxs-lookup"><span data-stu-id="a1328-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="a1328-119">Однако следует убедиться, что они существуют и что они содержат правильные значения для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="a1328-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="a1328-120">**JAVA_HOME** — эта переменная должна указывать на каталог, в который установлена среда выполнения Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="a1328-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="a1328-121">Например, в дистрибутиве Unix или Linux она должна иметь примерно такое значение: `/usr/lib/jvm/java-7-oracle`</span><span class="sxs-lookup"><span data-stu-id="a1328-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="a1328-122">В Windows значение будет приблизительно таким: `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="a1328-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="a1328-123">**PATH** — эта переменная должна содержать следующие пути:</span><span class="sxs-lookup"><span data-stu-id="a1328-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="a1328-124">**JAVA_HOME** или эквивалентный путь;</span><span class="sxs-lookup"><span data-stu-id="a1328-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="a1328-125">**JAVA_HOME\bin** или эквивалентный путь.</span><span class="sxs-lookup"><span data-stu-id="a1328-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="a1328-126">Каталог, в который установлено ПО Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="a1328-127">Создание проекта Maven</span><span class="sxs-lookup"><span data-stu-id="a1328-127">Create a Maven project</span></span>

<span data-ttu-id="a1328-128">В командной строке введите следующую команду для создания проекта Maven с именем **WordCount**.</span><span class="sxs-lookup"><span data-stu-id="a1328-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="a1328-129">При использовании PowerShell параметры `-D` необходимо заключить в кавычки.</span><span class="sxs-lookup"><span data-stu-id="a1328-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="a1328-130">Эта команда создает каталог с именем `WordCount` в текущем расположении, содержащий базовый проект Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="a1328-131">Каталог `WordCount` содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="a1328-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="a1328-132">`pom.xml` содержит параметры для проекта Maven;</span><span class="sxs-lookup"><span data-stu-id="a1328-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="a1328-133">`src\main\java\com\microsoft\example` содержит код приложения;</span><span class="sxs-lookup"><span data-stu-id="a1328-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="a1328-134">`src\test\java\com\microsoft\example` содержит тесты для приложения.</span><span class="sxs-lookup"><span data-stu-id="a1328-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="a1328-135">Удаление созданного примера кода</span><span class="sxs-lookup"><span data-stu-id="a1328-135">Remove the generated example code</span></span>

<span data-ttu-id="a1328-136">Удалите созданные тесты и файлы приложения:</span><span class="sxs-lookup"><span data-stu-id="a1328-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="a1328-137">**src\test\java\com\microsoft\example\AppTest.java**;</span><span class="sxs-lookup"><span data-stu-id="a1328-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="a1328-138">**src\main\java\com\microsoft\example\App.java**.</span><span class="sxs-lookup"><span data-stu-id="a1328-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="a1328-139">Добавление репозиториев Maven</span><span class="sxs-lookup"><span data-stu-id="a1328-139">Add Maven repositories</span></span>

<span data-ttu-id="a1328-140">Решение HDInsight основано на платформе данных Hortonworks Data Platform (HDP), поэтому мы рекомендуем использовать репозиторий Hortonworks для скачивания зависимостей для проектов Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="a1328-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="a1328-141">Добавьте в файл __pom.xml__ приведенный ниже код XML после строки `<url>http://maven.apache.org</url>`.</span><span class="sxs-lookup"><span data-stu-id="a1328-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="a1328-142">Добавление свойств</span><span class="sxs-lookup"><span data-stu-id="a1328-142">Add properties</span></span>

<span data-ttu-id="a1328-143">Maven позволяет определить значения на уровне проекта, которые называются свойствами.</span><span class="sxs-lookup"><span data-stu-id="a1328-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="a1328-144">Добавьте в файл __pom.xml__ приведенный ниже текст после строки `</repositories>`.</span><span class="sxs-lookup"><span data-stu-id="a1328-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="a1328-145">Теперь это значение можно использовать в других разделах `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="a1328-146">Например, при указании версии компонентов Storm, можно использовать `${storm.version}` вместо жестко запрограммированного значения.</span><span class="sxs-lookup"><span data-stu-id="a1328-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="a1328-147">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="a1328-147">Add dependencies</span></span>

<span data-ttu-id="a1328-148">Добавьте зависимость для компонентов Storm.</span><span class="sxs-lookup"><span data-stu-id="a1328-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="a1328-149">Откройте файл `pom.xml` и добавьте следующий код в раздел `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="a1328-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="a1328-150">Во время компиляции Maven использует эту информацию для поиска `storm-core` в репозитории Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="a1328-151">Сначала выполняется поиск в репозитории на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a1328-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="a1328-152">Если файлы отсутствуют, Maven скачает их из общедоступного репозитория Maven и сохранит в локальном репозитории.</span><span class="sxs-lookup"><span data-stu-id="a1328-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-153">Обратите внимание на строку `<scope>provided</scope>` в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a1328-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="a1328-154">Она указывает Maven, что **storm-core** нужно исключить из всех созданных JAR-файлов, так как этот элемент предоставит система.</span><span class="sxs-lookup"><span data-stu-id="a1328-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="a1328-155">Конфигурация построения</span><span class="sxs-lookup"><span data-stu-id="a1328-155">Build configuration</span></span>

<span data-ttu-id="a1328-156">Подключаемые модули Maven позволяют настроить этапы сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="a1328-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="a1328-157">Например, способ компиляции проекта или его упаковки в JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="a1328-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="a1328-158">Откройте файл `pom.xml` и добавьте следующий код непосредственно над строкой `</project>`:</span><span class="sxs-lookup"><span data-stu-id="a1328-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="a1328-159">Этот раздел используется для добавления подключаемых модулей, ресурсов и других параметров конфигурации сборки.</span><span class="sxs-lookup"><span data-stu-id="a1328-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="a1328-160">Все справочные материалы по файлу **pom.xml** см. по адресу [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="a1328-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="a1328-161">Добавление подключаемых модулей</span><span class="sxs-lookup"><span data-stu-id="a1328-161">Add plug-ins</span></span>

<span data-ttu-id="a1328-162">Для топологий Apache Storm, реализованных на языке Java, удобен [подключаемый модуль Exec Maven](http://www.mojohaus.org/exec-maven-plugin/), так как он позволяет легко запускать топологию локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="a1328-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="a1328-163">Добавьте следующий код в раздел `<plugins>` файла `pom.xml`, чтобы включить в него подключаемый модуль Exec Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="a1328-164">Другим полезным подключаемым модулем является  [Apache Maven Compiler](http://maven.apache.org/plugins/maven-compiler-plugin/), который используется для изменения параметров компиляции.</span><span class="sxs-lookup"><span data-stu-id="a1328-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="a1328-165">Он нам нужен, чтобы изменить версию Java, используемую Maven для исходного и целевого объекта приложения.</span><span class="sxs-lookup"><span data-stu-id="a1328-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="a1328-166">Для HDInsight __3.4 или более ранней версии__ задайте версию __1.7__ в качестве исходной и целевой версий Java.</span><span class="sxs-lookup"><span data-stu-id="a1328-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="a1328-167">Для HDInsight __3.5__ в качестве исходной и целевой версий Java задайте версию __1.8__.</span><span class="sxs-lookup"><span data-stu-id="a1328-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="a1328-168">Добавьте следующий код в раздел `<plugins>` файла `pom.xml`, чтобы добавить в него подключаемый модуль Apache Maven Compiler.</span><span class="sxs-lookup"><span data-stu-id="a1328-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="a1328-169">Этот пример задает версию 1.8, поэтому целевой версией HDInsight является 3.5.</span><span class="sxs-lookup"><span data-stu-id="a1328-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="a1328-170">Настройка ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1328-170">Configure resources</span></span>

<span data-ttu-id="a1328-171">Раздел ресурсов позволяет включать не связанные с кодом ресурсы, такие как файлы конфигурации, необходимые для компонентов топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="a1328-172">Например, добавьте следующий текст в раздел `<resources>` файла pom.xml.</span><span class="sxs-lookup"><span data-stu-id="a1328-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="a1328-173">При этом в корневую папку проекта (`${basedir}`) будет добавлен каталог ресурсов как расположение, содержащее ресурсы и файл `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="a1328-174">Этот файл используется для настройки того, какая информация записывается топологией.</span><span class="sxs-lookup"><span data-stu-id="a1328-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="a1328-175">Создание топологии</span><span class="sxs-lookup"><span data-stu-id="a1328-175">Create the topology</span></span>

<span data-ttu-id="a1328-176">Топология Apache Storm на платформе Java состоит из трех компонентов, которые необходимо создать или указать как зависимость.</span><span class="sxs-lookup"><span data-stu-id="a1328-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="a1328-177">**Воронки**— чтение данных из внешних источников и отправка потоков данных в топологию.</span><span class="sxs-lookup"><span data-stu-id="a1328-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="a1328-178">**Сита**— выполнение обработки потоков, поступающих из воронок или других сит, и создание одного или нескольких потоков.</span><span class="sxs-lookup"><span data-stu-id="a1328-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="a1328-179">**Топология**— определяет взаимное расположение воронок и сит и предоставляет точку входа для топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="a1328-180">Создание «воронки»</span><span class="sxs-lookup"><span data-stu-id="a1328-180">Create the spout</span></span>

<span data-ttu-id="a1328-181">Чтобы снизить требования к настройке внешних источников данных, следующая воронка просто выдает случайные предложения.</span><span class="sxs-lookup"><span data-stu-id="a1328-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="a1328-182">Это измененная версия воронки, представленная в [примерах Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="a1328-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-183">Пример воронки, которая считывает информацию из внешнего источника данных, см. в одном из следующих примеров.</span><span class="sxs-lookup"><span data-stu-id="a1328-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="a1328-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java)— пример воронки, считывающей информацию из Twitter.</span><span class="sxs-lookup"><span data-stu-id="a1328-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="a1328-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka)— воронка, считывающая информацию из Kafka.</span><span class="sxs-lookup"><span data-stu-id="a1328-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="a1328-186">Создайте для элемента spout файл с именем `RandomSentenceSpout.java` в каталоге `src\main\java\com\microsoft\example`, а затем используйте следующий код Java в качестве содержимого этого файла:</span><span class="sxs-lookup"><span data-stu-id="a1328-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="a1328-187">Хотя в данной топологии используется только одна воронка, в других топологиях их может быть несколько. При этом данные могут поступать в топологию из различных источников.</span><span class="sxs-lookup"><span data-stu-id="a1328-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="a1328-188">Создание «сит»</span><span class="sxs-lookup"><span data-stu-id="a1328-188">Create the bolts</span></span>

<span data-ttu-id="a1328-189">Сита выполняют обработку данных.</span><span class="sxs-lookup"><span data-stu-id="a1328-189">Bolts handle the data processing.</span></span> <span data-ttu-id="a1328-190">Эта топология включает два сита.</span><span class="sxs-lookup"><span data-stu-id="a1328-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="a1328-191">**SplitSentence** — разделяет предложения, отправленные **RandomSentenceSpout**, на отдельные слова;</span><span class="sxs-lookup"><span data-stu-id="a1328-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="a1328-192">**WordCount**— подсчитывает частоту употребления каждого слова.</span><span class="sxs-lookup"><span data-stu-id="a1328-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-193">Элементы bolt могут выполнять любые операции, например вычисление, сохранение, а также взаимодействие с внешними компонентами.</span><span class="sxs-lookup"><span data-stu-id="a1328-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="a1328-194">В каталоге `src\main\java\com\microsoft\example` создайте два файла — `SplitSentence.java` и `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="a1328-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="a1328-195">В качестве содержимого файлов добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="a1328-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="a1328-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="a1328-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="a1328-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="a1328-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-the-topology"></a><span data-ttu-id="a1328-198">Определение топологии</span><span class="sxs-lookup"><span data-stu-id="a1328-198">Define the topology</span></span>

<span data-ttu-id="a1328-199">Топология связывает воронки и сита на диаграмме, определяя порядок обмена данными между компонентами.</span><span class="sxs-lookup"><span data-stu-id="a1328-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="a1328-200">Она также предоставляет указания по обеспечению параллелизма, которые Storm использует при создании экземпляров компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="a1328-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="a1328-201">На рисунке ниже приведена базовая диаграмма компонентов этой топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![диаграмма, показывающая упорядочение воронок и сит](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="a1328-203">Для реализации топологии создайте файл с именем `WordCountTopology.java` в каталоге `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="a1328-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="a1328-204">Добавьте в файл следующий код Java:</span><span class="sxs-lookup"><span data-stu-id="a1328-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="a1328-205">Настройка журнала</span><span class="sxs-lookup"><span data-stu-id="a1328-205">Configure logging</span></span>

<span data-ttu-id="a1328-206">Storm использует Apache Log4j для записи информации в журнал.</span><span class="sxs-lookup"><span data-stu-id="a1328-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="a1328-207">Если не настроить ведение журналов, то топология будет выдавать диагностические сведения.</span><span class="sxs-lookup"><span data-stu-id="a1328-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="a1328-208">Чтобы управлять записываемыми сведениями, создайте в каталоге `resources` файл с именем `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="a1328-209">Используйте следующий код XML в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="a1328-209">Use the following XML as the contents of the file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="a1328-210">Это позволит настроить новое средство ведения журнала для класса `com.microsoft.example`, который включает компоненты в этом примере топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="a1328-211">Для этого средства ведения журнала задается уровень трассировки, таким образом будут протоколироваться все сведения о журнале, генерируемые компонентами данной топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="a1328-212">В разделе `<Root level="error">` для корневого уровня ведения журнала (все, что не находится в файле `com.microsoft.example`) настраивается регистрация только сведений об ошибках.</span><span class="sxs-lookup"><span data-stu-id="a1328-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="a1328-213">Дополнительные сведения о настройке ведения журнала с помощью Log4j см. по адресу [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="a1328-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="a1328-214">Storm 0.10.0 и более поздних версий использует Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="a1328-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="a1328-215">В предыдущих версиях Storm использовался выпуск Log4j 1.x, в котором для настройки журнала применялся другой формат.</span><span class="sxs-lookup"><span data-stu-id="a1328-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="a1328-216">Сведения о предыдущих версиях конфигурации см. по адресу [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="a1328-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="a1328-217">Локальная проверка топологии</span><span class="sxs-lookup"><span data-stu-id="a1328-217">Test the topology locally</span></span>

<span data-ttu-id="a1328-218">После сохранения файлов используйте следующую команду для локального тестирования топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="a1328-219">Во время их выполнения топология отображает сведения о запуске.</span><span class="sxs-lookup"><span data-stu-id="a1328-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="a1328-220">Следующий текст представляет собой пример выходных данных подсчета слов:</span><span class="sxs-lookup"><span data-stu-id="a1328-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="a1328-221">Этот пример журнала означает, что слово "и" было отправлено 113 раз.</span><span class="sxs-lookup"><span data-stu-id="a1328-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="a1328-222">Количество продолжает увеличиваться, пока выполняется топология, так как элемент spout постоянно отправляет одни и те же предложения.</span><span class="sxs-lookup"><span data-stu-id="a1328-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="a1328-223">Между отправлениями данных о словах и их количестве проходит 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="a1328-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="a1328-224">Компонент **WordCount** настроен для отправки данных, только когда прибывает временной кортеж.</span><span class="sxs-lookup"><span data-stu-id="a1328-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="a1328-225">Он запрашивает доставку таких кортежей каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="a1328-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="a1328-226">Преобразование топологии для Flux</span><span class="sxs-lookup"><span data-stu-id="a1328-226">Convert the topology to Flux</span></span>

<span data-ttu-id="a1328-227">Flux — это новая платформа, доступная в Storm 0.10.0 и более поздних версий, которая позволяет отделить конфигурацию от реализации.</span><span class="sxs-lookup"><span data-stu-id="a1328-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="a1328-228">Компоненты по-прежнему определяются на языке Java, но топология определяется с использованием файла YAML.</span><span class="sxs-lookup"><span data-stu-id="a1328-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="a1328-229">Вы можете упаковать определение топологии по умолчанию в проекте или же использовать автономный файл при отправке топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="a1328-230">При отправке топологии в Storm можно использовать переменные среды или файлы конфигурации для заполнения значений в определении топологии YAML.</span><span class="sxs-lookup"><span data-stu-id="a1328-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="a1328-231">Файл YAML определяет компоненты для топологии и поток данных между ними.</span><span class="sxs-lookup"><span data-stu-id="a1328-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="a1328-232">Файл YAML можно добавить как часть JAR-файла или можно использовать внешний файл YAML.</span><span class="sxs-lookup"><span data-stu-id="a1328-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="a1328-233">Дополнительные сведения о платформе Flux см. в статье, посвященной [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="a1328-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="a1328-234">Из-за [ошибки (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) в Storm 1.0.1 может потребоваться установить [среду разработки Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) для локального запуска топологий Flux.</span><span class="sxs-lookup"><span data-stu-id="a1328-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="a1328-235">Удалите файл `WordCountTopology.java` из проекта.</span><span class="sxs-lookup"><span data-stu-id="a1328-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="a1328-236">Ранее он определял топологию, но с платформой Flux он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="a1328-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="a1328-237">В каталоге `resources` создайте файл с именем `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="a1328-238">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="a1328-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="a1328-239">Внесите следующие изменения в файл `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="a1328-240">Добавьте следующую новую зависимость в разделе `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="a1328-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="a1328-241">Добавьте следующий подключаемый модуль в раздел `<plugins>`:</span><span class="sxs-lookup"><span data-stu-id="a1328-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="a1328-242">Этот подключаемый модуль обрабатывает создание пакета (JAR-файла) для проекта и применяет некоторые преобразования, характерные для Flux, во время создания пакета.</span><span class="sxs-lookup"><span data-stu-id="a1328-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer to it as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
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
        ```

   * <span data-ttu-id="a1328-243">В разделе **exec-maven-plugin** `<configuration>` измените значение для `<mainClass>` на `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="a1328-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="a1328-244">Таким образом, Flux сможет обрабатывать выполнение топологии при ее локальном запуске в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="a1328-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="a1328-245">В разделе `<resources>` добавьте следующий код в раздел `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="a1328-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="a1328-246">Он включает файл YAML, который определяет топологию как часть проекта.</span><span class="sxs-lookup"><span data-stu-id="a1328-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="a1328-247">Локальная проверка топологии Flux</span><span class="sxs-lookup"><span data-stu-id="a1328-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="a1328-248">Скомпилируйте и выполните топологию Flux с помощью Maven, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1328-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="a1328-249">При использовании PowerShell воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a1328-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="a1328-250">Эта команда не выполняется, если топология использует ресурсы Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="a1328-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="a1328-251">Причиной этого является ошибка [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="a1328-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="a1328-252">Вместо этого [установите Storm в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) и используйте следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="a1328-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="a1328-253">Если вы [установили Storm в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), вместо этого можно использовать приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="a1328-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="a1328-254">Параметр `--local` выполняет топологию в локальном режиме в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="a1328-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="a1328-255">Параметр `-R /topology.yaml` использует файловый ресурс `topology.yaml` из JAR-файла для определения топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="a1328-256">Во время их выполнения топология отображает сведения о запуске.</span><span class="sxs-lookup"><span data-stu-id="a1328-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="a1328-257">Ниже приведен пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a1328-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="a1328-258">Пакеты со сведениями журналов отправляются раз в 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="a1328-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="a1328-259">Создайте копию файла `topology.yaml` из проекта.</span><span class="sxs-lookup"><span data-stu-id="a1328-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="a1328-260">Дайте новому файлу имя `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a1328-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="a1328-261">В файле `newtopology.yaml` найдите следующий раздел и измените значение `10` на `5`.</span><span class="sxs-lookup"><span data-stu-id="a1328-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="a1328-262">Это изменит интервал между отправкой пакетов с данными о количестве слов с 10 до 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="a1328-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="a1328-263">Или, если в среде разработки имеется Storm, вы можете выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a1328-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="a1328-264">Измените `/path/to/newtopology.yaml` на путь к файлу newtopology.yaml, созданному на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a1328-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="a1328-265">Эта команда использует файл newtopology.yaml в качестве определения топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="a1328-266">Так как параметр `compile` не добавлен, Maven использует версию проекта, созданного на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="a1328-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="a1328-267">После запуска топологии вы, возможно, заметили, что время между отправлением пакетов изменилось с учетом значений в файле newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="a1328-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="a1328-268">Таким образом, вы видите, что можно изменить конфигурацию в файле YAML, не выполняя повторную компиляцию топологии.</span><span class="sxs-lookup"><span data-stu-id="a1328-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="a1328-269">Дополнительные сведения об этих и других возможностях платформы Flux см. в статье, посвященной [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="a1328-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="a1328-270">Trident</span><span class="sxs-lookup"><span data-stu-id="a1328-270">Trident</span></span>

<span data-ttu-id="a1328-271">Trident — это высокоуровневая абстракция, предоставляемая Storm.</span><span class="sxs-lookup"><span data-stu-id="a1328-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="a1328-272">Он поддерживает обработку с отслеживанием состояний.</span><span class="sxs-lookup"><span data-stu-id="a1328-272">It supports stateful processing.</span></span> <span data-ttu-id="a1328-273">Основное преимущество Trident заключается в том, что эта технология гарантирует одноразовую обработку каждого сообщения, которое входит в топологию.</span><span class="sxs-lookup"><span data-stu-id="a1328-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="a1328-274">Без использования Trident топология только гарантирует, что каждое сообщение обрабатывается по крайней мере один раз.</span><span class="sxs-lookup"><span data-stu-id="a1328-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="a1328-275">Существуют также другие отличия, например встроенные компоненты, которые можно использовать вместо создания сит.</span><span class="sxs-lookup"><span data-stu-id="a1328-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="a1328-276">На самом деле элементы bolt заменяются не столь общими компонентами, например фильтрами, проекциями и функциями.</span><span class="sxs-lookup"><span data-stu-id="a1328-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="a1328-277">Приложения Trident можно создавать с помощью проектов Maven.</span><span class="sxs-lookup"><span data-stu-id="a1328-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="a1328-278">Для этого используются те же основные действия, приведенные ранее в этой статье, отличается только код.</span><span class="sxs-lookup"><span data-stu-id="a1328-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="a1328-279">Сейчас Trident нельзя использовать с платформой Flux.</span><span class="sxs-lookup"><span data-stu-id="a1328-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="a1328-280">Дополнительные сведения о Trident см. в статье [Обзор API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html) (на английском языке).</span><span class="sxs-lookup"><span data-stu-id="a1328-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="a1328-281">Пример приложения Trident см. в статье [Определение популярных тем в Twitter с помощью Apache Storm в HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="a1328-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1328-282">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1328-282">Next Steps</span></span>

<span data-ttu-id="a1328-283">Вы узнали, как создавать топологии Storm с помощью Java.</span><span class="sxs-lookup"><span data-stu-id="a1328-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="a1328-284">Теперь ознакомьтесь со следующими статьями.</span><span class="sxs-lookup"><span data-stu-id="a1328-284">Now learn how to:</span></span>

* [<span data-ttu-id="a1328-285">Развертывание топологий Apache Storm в HDInsight и управление ими</span><span class="sxs-lookup"><span data-stu-id="a1328-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="a1328-286">Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1328-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="a1328-287">Другие примеры топологий Storm см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a1328-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

