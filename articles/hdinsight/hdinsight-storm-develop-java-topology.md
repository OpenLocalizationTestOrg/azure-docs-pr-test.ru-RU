---
title: "aaaApache Storm пример топологии Java - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Apache Storm топологии на Java, создав слово подсчета топологии."
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
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="2094c-104">Создание топологии Apache Storm на языке Java</span><span class="sxs-lookup"><span data-stu-id="2094c-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="2094c-105">Узнайте, как toocreate топологии на основе Java применения Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="2094c-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="2094c-106">Вы создадите топологию Storm, реализующую приложение подсчета слов.</span><span class="sxs-lookup"><span data-stu-id="2094c-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="2094c-107">Используется проект hello Maven toobuild и пакета.</span><span class="sxs-lookup"><span data-stu-id="2094c-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="2094c-108">Затем вы узнаете, как с помощью топологии hello toodefine hello framework определен.</span><span class="sxs-lookup"><span data-stu-id="2094c-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-109">framework определен Hello Storm 0.10.0 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2094c-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="2094c-110">Storm 0.10.0 доступна в HDInsight 3.3 и 3.4.</span><span class="sxs-lookup"><span data-stu-id="2094c-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="2094c-111">После завершения шагов hello в этом документе, можно развернуть hello топологии tooApache Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2094c-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-112">Полную версию создан в этом документе примеры топологии Storm hello доступен на [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="2094c-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2094c-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2094c-113">Prerequisites</span></span>

* [<span data-ttu-id="2094c-114">Java Developer Kit (JDK) версии 7</span><span class="sxs-lookup"><span data-stu-id="2094c-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="2094c-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): система сборки проектов для Java.</span><span class="sxs-lookup"><span data-stu-id="2094c-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="2094c-116">Текстовый редактор или интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="2094c-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="2094c-117">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="2094c-117">Configure environment variables</span></span>

<span data-ttu-id="2094c-118">Hello следующие переменные среды можно задать при установке Java и hello JDK.</span><span class="sxs-lookup"><span data-stu-id="2094c-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="2094c-119">Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="2094c-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="2094c-120">**JAVA_HOME** -должен указывать toohello каталог, где установлен hello среда выполнения Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="2094c-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="2094c-121">Например, при распределении Unix или Linux, возможно только значение, схожее слишком`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="2094c-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="2094c-122">В Windows он будет иметь значение, схожее слишком`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="2094c-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="2094c-123">**ПУТЬ** -должна содержать hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="2094c-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="2094c-124">**JAVA_HOME** (или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="2094c-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="2094c-125">**JAVA_HOME\bin** (или эквивалентный путь hello)</span><span class="sxs-lookup"><span data-stu-id="2094c-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="2094c-126">Hello каталог для установки Maven</span><span class="sxs-lookup"><span data-stu-id="2094c-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="2094c-127">Создание проекта Maven</span><span class="sxs-lookup"><span data-stu-id="2094c-127">Create a Maven project</span></span>

<span data-ttu-id="2094c-128">Из командной строки hello, используйте hello следующая команда toocreate Maven проект с именем **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="2094c-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="2094c-129">При использовании PowerShell параметры `-D` необходимо заключить в кавычки.</span><span class="sxs-lookup"><span data-stu-id="2094c-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="2094c-130">Эта команда создает каталог с именем `WordCount` hello текущей позиции, которая содержит базовый проект Maven.</span><span class="sxs-lookup"><span data-stu-id="2094c-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="2094c-131">Hello `WordCount` каталог содержит hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2094c-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="2094c-132">`pom.xml`: Содержит параметры для проекта Maven hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="2094c-133">`src\main\java\com\microsoft\example` содержит код приложения;</span><span class="sxs-lookup"><span data-stu-id="2094c-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="2094c-134">`src\test\java\com\microsoft\example` содержит тесты для приложения.</span><span class="sxs-lookup"><span data-stu-id="2094c-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="2094c-135">Удалить созданные hello пример кода</span><span class="sxs-lookup"><span data-stu-id="2094c-135">Remove hello generated example code</span></span>

<span data-ttu-id="2094c-136">Удалите тест создан hello и файлы приложения hello:</span><span class="sxs-lookup"><span data-stu-id="2094c-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="2094c-137">**src\test\java\com\microsoft\example\AppTest.java**;</span><span class="sxs-lookup"><span data-stu-id="2094c-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="2094c-138">**src\main\java\com\microsoft\example\App.java**.</span><span class="sxs-lookup"><span data-stu-id="2094c-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="2094c-139">Добавление репозиториев Maven</span><span class="sxs-lookup"><span data-stu-id="2094c-139">Add Maven repositories</span></span>

<span data-ttu-id="2094c-140">HDInsight основан на hello Hortonworks Data Platform (HDP), поэтому мы рекомендуем использовать hello Hortonworks репозитория toodownload зависимостей для проектов Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="2094c-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="2094c-141">В hello __pom.xml__ файл, добавьте следующий XML-код после hello hello `<url>http://maven.apache.org</url>` строки:</span><span class="sxs-lookup"><span data-stu-id="2094c-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="2094c-142">Добавление свойств</span><span class="sxs-lookup"><span data-stu-id="2094c-142">Add properties</span></span>

<span data-ttu-id="2094c-143">Maven позволяет toodefine значения на уровне проекта, называются свойствами.</span><span class="sxs-lookup"><span data-stu-id="2094c-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="2094c-144">В hello __pom.xml__, добавьте следующий текст после hello hello `</repositories>` строки:</span><span class="sxs-lookup"><span data-stu-id="2094c-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="2094c-145">Теперь можно использовать это значение в других разделах hello `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="2094c-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="2094c-146">Например, при определении версии hello Storm компонентов, можно использовать `${storm.version}` вместо жесткого программирования значение.</span><span class="sxs-lookup"><span data-stu-id="2094c-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="2094c-147">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="2094c-147">Add dependencies</span></span>

<span data-ttu-id="2094c-148">Добавьте зависимость для компонентов Storm.</span><span class="sxs-lookup"><span data-stu-id="2094c-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="2094c-149">Откройте hello `pom.xml` и добавьте следующий код в hello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="2094c-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="2094c-150">Во время компиляции, Maven использует этот toolook сведения `storm-core` в репозиторий Maven hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="2094c-151">Сначала выполняет поиск в репозитории hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2094c-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="2094c-152">Если файлы hello не существует, Maven загружает их из открытого репозитория Maven hello и сохраняет их в локальном хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-153">Обратите внимание hello `<scope>provided</scope>` строки в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2094c-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="2094c-154">Этот параметр указывает Maven tooexclude **storm-core** из любые JAR-файлы, которые создаются, так как она задается системой hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="2094c-155">Конфигурация построения</span><span class="sxs-lookup"><span data-stu-id="2094c-155">Build configuration</span></span>

<span data-ttu-id="2094c-156">Подключаемые модули maven разрешить toocustomize hello этапы построения проекта hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="2094c-157">Например, способ компиляции проекта hello или как toopackage его в JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="2094c-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="2094c-158">Откройте hello `pom.xml` и добавьте следующий код непосредственно над hello hello `</project>` строки.</span><span class="sxs-lookup"><span data-stu-id="2094c-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="2094c-159">Этот раздел представляет используется tooadd подключаемые модули, ресурсы и другие параметры конфигурации сборки.</span><span class="sxs-lookup"><span data-stu-id="2094c-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="2094c-160">Полную справочную hello **pom.xml** файла см. в разделе [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="2094c-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="2094c-161">Добавление подключаемых модулей</span><span class="sxs-lookup"><span data-stu-id="2094c-161">Add plug-ins</span></span>

<span data-ttu-id="2094c-162">Для топологий Apache Storm реализовано на языке Java, hello [подключаемый модуль Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) полезно, так как она допускает tooeasily выполнение топологии hello локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="2094c-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="2094c-163">Добавьте следующие toohello hello `<plugins>` раздел hello `pom.xml` файл подключаемого модуля Exec Maven hello tooinclude:</span><span class="sxs-lookup"><span data-stu-id="2094c-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="2094c-164">Другой полезные подключаемый модуль hello [Apache Maven компилятора, подключаемый модуль](http://maven.apache.org/plugins/maven-compiler-plugin/), который будет использоваться toochange параметры компиляции.</span><span class="sxs-lookup"><span data-stu-id="2094c-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="2094c-165">изменения Hello hello версии Java, использующего Maven для hello исходного и конечного приложения.</span><span class="sxs-lookup"><span data-stu-id="2094c-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="2094c-166">Для HDInsight __3,4 или более ранней версии__, задать hello источник и целевой too__1.7__ версии Java.</span><span class="sxs-lookup"><span data-stu-id="2094c-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="2094c-167">Для HDInsight __3.5__, задать hello источник и целевой too__1.8__ версии Java.</span><span class="sxs-lookup"><span data-stu-id="2094c-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="2094c-168">Добавить после текста hello hello `<plugins>` раздел hello `pom.xml` файл подключаемого модуля Apache Maven компилятора hello tooinclude.</span><span class="sxs-lookup"><span data-stu-id="2094c-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="2094c-169">В этом примере указывает 1.8, поэтому hello целевой HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="2094c-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="2094c-170">Настройка ресурсов</span><span class="sxs-lookup"><span data-stu-id="2094c-170">Configure resources</span></span>

<span data-ttu-id="2094c-171">раздел ресурсов Hello позволяет ресурсы не кода tooinclude например файлов конфигурации, необходимых компонентов в топологии hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="2094c-172">Например, добавьте после текста hello hello `<resources>` раздел hello "pom.xml файла.</span><span class="sxs-lookup"><span data-stu-id="2094c-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="2094c-173">В этом примере добавляется каталог ресурсов hello в корневой hello hello проекта (`${basedir}`) как расположение, содержащий ресурсы и включает hello файл с именем `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="2094c-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="2094c-174">Этот файл является используется tooconfigure, какие сведения записываются hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="2094c-175">Создание топологии hello</span><span class="sxs-lookup"><span data-stu-id="2094c-175">Create hello topology</span></span>

<span data-ttu-id="2094c-176">Топология Apache Storm на платформе Java состоит из трех компонентов, которые необходимо создать или указать как зависимость.</span><span class="sxs-lookup"><span data-stu-id="2094c-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="2094c-177">**Spouts**: считывает данные из внешних источников и выдает потоков данных в топологии hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="2094c-178">**Сита**— выполнение обработки потоков, поступающих из воронок или других сит, и создание одного или нескольких потоков.</span><span class="sxs-lookup"><span data-stu-id="2094c-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="2094c-179">**Топология**: Определяет, как hello spouts и винты упорядочиваются и предоставляет точку входа hello hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="2094c-180">Создание hello spout</span><span class="sxs-lookup"><span data-stu-id="2094c-180">Create hello spout</span></span>

<span data-ttu-id="2094c-181">Здравствуйте tooreduce требования к настройке внешних источников данных, выполнив spout просто выдает случайных предложений.</span><span class="sxs-lookup"><span data-stu-id="2094c-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="2094c-182">Это измененная версия spout, который входит в состав hello [примеры начального уровня Storm](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="2094c-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-183">Пример spout, который считывает данные из внешнего источника данных см. следующие примеры hello:</span><span class="sxs-lookup"><span data-stu-id="2094c-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="2094c-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java)— пример воронки, считывающей информацию из Twitter.</span><span class="sxs-lookup"><span data-stu-id="2094c-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="2094c-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka)— воронка, считывающая информацию из Kafka.</span><span class="sxs-lookup"><span data-stu-id="2094c-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="2094c-186">Для hello spout, создайте файл с именем `RandomSentenceSpout.java` в hello `src\main\java\com\microsoft\example` hello каталог и использовать следующий код Java как hello содержимое:</span><span class="sxs-lookup"><span data-stu-id="2094c-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
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

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="2094c-187">Несмотря на то, что данная топология использует только один spout, другие могут иметь несколько, веб-канала данных из различных источников в топологию hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="2094c-188">Создание винты hello</span><span class="sxs-lookup"><span data-stu-id="2094c-188">Create hello bolts</span></span>

<span data-ttu-id="2094c-189">Винты обрабатывать hello обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2094c-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="2094c-190">Эта топология включает два сита.</span><span class="sxs-lookup"><span data-stu-id="2094c-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="2094c-191">**SplitSentence**: разделяет hello предложений, генерируемой **RandomSentenceSpout** на отдельные слова.</span><span class="sxs-lookup"><span data-stu-id="2094c-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="2094c-192">**WordCount**— подсчитывает частоту употребления каждого слова.</span><span class="sxs-lookup"><span data-stu-id="2094c-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-193">Винты можно выполнять никаких действий, например, вычисления, сохранения или взаимодействии компонентов tooexternal.</span><span class="sxs-lookup"><span data-stu-id="2094c-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="2094c-194">Создайте два новых файла `SplitSentence.java` и `WordCount.java` в hello `src\main\java\com\microsoft\example` каталога.</span><span class="sxs-lookup"><span data-stu-id="2094c-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="2094c-195">Используйте hello после текста как hello содержимое для hello файлов:</span><span class="sxs-lookup"><span data-stu-id="2094c-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="2094c-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="2094c-196">SplitSentence</span></span>

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

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
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

#### <a name="wordcount"></a><span data-ttu-id="2094c-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="2094c-197">WordCount</span></span>

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
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
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
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
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

### <a name="define-hello-topology"></a><span data-ttu-id="2094c-198">Определение топологии hello</span><span class="sxs-lookup"><span data-stu-id="2094c-198">Define hello topology</span></span>

<span data-ttu-id="2094c-199">Топология Hello связывает hello spouts и болтов вместе в граф, который определяет порядок обмена данными между компонентами hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="2094c-200">Он также предоставляет указания параллелизма, которые Storm используется при создании экземпляров компонентов hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="2094c-201">Hello следующем рисунке показана базовая диаграмма графа hello компонентов для реализации этой топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![Схема отображение hello spouts и болтов упорядочение](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="2094c-203">tooimplement Здравствуйте топологии, создайте файл с именем `WordCountTopology.java` в hello `src\main\java\com\microsoft\example` каталога.</span><span class="sxs-lookup"><span data-stu-id="2094c-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="2094c-204">Используйте следующий пример кода Java как hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="2094c-205">Настройка журнала</span><span class="sxs-lookup"><span data-stu-id="2094c-205">Configure logging</span></span>

<span data-ttu-id="2094c-206">Storm использует Apache Log4j toolog сведения.</span><span class="sxs-lookup"><span data-stu-id="2094c-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="2094c-207">Если ведение журнала не задан, топологии hello выдает диагностические сведения.</span><span class="sxs-lookup"><span data-stu-id="2094c-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="2094c-208">toocontrol регистрируемых сведений, создайте файл с именем `log4j2.xml` в hello `resources` каталога.</span><span class="sxs-lookup"><span data-stu-id="2094c-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="2094c-209">Используйте следующий XML-код в виде hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="2094c-210">Этот XML-документ настраивает новое средство ведения журнала для hello `com.microsoft.example` класс, который включает в себя компоненты hello в данном примере топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="2094c-211">Установка уровня Hello tootrace для данного средства ведения журнала, включающую в себя каких данных испускаемый компоненты в этой топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="2094c-212">Hello `<Root level="error">` раздел настраивает hello корневой уровень ведения журнала (все, что не поддерживается в `com.microsoft.example`) tooonly сведения об ошибке журнала.</span><span class="sxs-lookup"><span data-stu-id="2094c-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="2094c-213">Дополнительные сведения о настройке ведения журнала с помощью Log4j см. по адресу [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="2094c-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="2094c-214">Storm 0.10.0 и более поздних версий использует Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="2094c-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="2094c-215">В предыдущих версиях Storm использовался выпуск Log4j 1.x, в котором для настройки журнала применялся другой формат.</span><span class="sxs-lookup"><span data-stu-id="2094c-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="2094c-216">Сведения о конфигурации старые hello. в разделе [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="2094c-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="2094c-217">Топология hello тестов локально</span><span class="sxs-lookup"><span data-stu-id="2094c-217">Test hello topology locally</span></span>

<span data-ttu-id="2094c-218">После сохранения файлов hello, используйте hello следующая команда tootest топологии hello локально.</span><span class="sxs-lookup"><span data-stu-id="2094c-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="2094c-219">Во время их выполнения топологии hello отображает информацию о запуске.</span><span class="sxs-lookup"><span data-stu-id="2094c-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="2094c-220">Hello следующий текст является примером count в формате word hello:</span><span class="sxs-lookup"><span data-stu-id="2094c-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="2094c-221">Этот пример журнала указывает это слово hello «и» было выдано 113 раз.</span><span class="sxs-lookup"><span data-stu-id="2094c-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="2094c-222">Hello количество продолжает toogo вверх, пока выполняется hello топологии, поскольку hello spout постоянно выдает hello одного предложения.</span><span class="sxs-lookup"><span data-stu-id="2094c-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="2094c-223">Между отправлениями данных о словах и их количестве проходит 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="2094c-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="2094c-224">Hello **WordCount** настроен компонент tooonly опускать сведения о прибытии кортеж делений.</span><span class="sxs-lookup"><span data-stu-id="2094c-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="2094c-225">Он запрашивает доставку таких кортежей каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="2094c-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="2094c-226">Преобразовать tooFlux топологии hello</span><span class="sxs-lookup"><span data-stu-id="2094c-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="2094c-227">Поток — это новая платформа с Storm 0.10.0 и более поздних версий, позволяющий конфигурации tooseparate от реализации.</span><span class="sxs-lookup"><span data-stu-id="2094c-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="2094c-228">Компоненты по-прежнему определяются на языке Java, но определяются с помощью файла YAML hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="2094c-229">Пакет определения топологии по умолчанию вместе с проектом или использовать отдельный файл при отправке hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="2094c-230">При отправке tooStorm топологии hello, можно использовать переменные среды или значения toopopulate файлы конфигурации в hello YAML определения топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="2094c-231">файл YAML Hello определяет hello toouse компоненты топологии hello и hello потока данных между ними.</span><span class="sxs-lookup"><span data-stu-id="2094c-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="2094c-232">Можно включить файл YAML как часть hello jar-файл, или можно использовать внешний файл YAML.</span><span class="sxs-lookup"><span data-stu-id="2094c-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="2094c-233">Дополнительные сведения о платформе Flux см. в статье, посвященной [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="2094c-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="2094c-234">Из-за tooa [ошибки (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) с урагана 1.0.1, может потребоваться tooinstall [среды разработки Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun топологии определен локально.</span><span class="sxs-lookup"><span data-stu-id="2094c-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="2094c-235">Переместить hello `WordCountTopology.java` файл из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="2094c-236">Ранее этот файл определен hello топологии, но не требуется с меняется.</span><span class="sxs-lookup"><span data-stu-id="2094c-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="2094c-237">В hello `resources` каталога, создайте файл с именем `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="2094c-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="2094c-238">Используйте hello после текста как hello содержимое этого файла.</span><span class="sxs-lookup"><span data-stu-id="2094c-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
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
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="2094c-239">Сделать следующие изменения toohello hello `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="2094c-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="2094c-240">Добавьте следующие новые зависимости в hello hello `<dependencies>` раздела:</span><span class="sxs-lookup"><span data-stu-id="2094c-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="2094c-241">Добавить подключаемый модуль toohello следующие hello `<plugins>` раздела.</span><span class="sxs-lookup"><span data-stu-id="2094c-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="2094c-242">Этот подключаемый модуль обрабатывает hello Создание пакета (jar-файл) для проекта hello и применяет определенные tooFlux некоторые преобразования при создании пакета hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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
                    <!-- We're using Flux, so refer tooit as main -->
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

   * <span data-ttu-id="2094c-243">В hello **exec maven подключаемый модуль** `<configuration>` измените значение hello `<mainClass>` слишком`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="2094c-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="2094c-244">Этот параметр позволяет toohandle меняется локальное выполнение топологии hello в разработке.</span><span class="sxs-lookup"><span data-stu-id="2094c-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="2094c-245">В hello `<resources>` добавьте следующие toohello hello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="2094c-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="2094c-246">Этот XML-документ включает файл YAML hello, который определяет топологию hello в рамках проекта hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="2094c-247">Топология меняется hello тестов локально</span><span class="sxs-lookup"><span data-stu-id="2094c-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="2094c-248">Используйте следующие toocompile hello и выполните топологии меняется hello, с помощью Maven:</span><span class="sxs-lookup"><span data-stu-id="2094c-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="2094c-249">Если вы используете PowerShell hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2094c-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="2094c-250">Эта команда не выполняется, если топология использует ресурсы Storm 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="2094c-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="2094c-251">Причиной этого является ошибка [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="2094c-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="2094c-252">Вместо этого [установить ураган в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) и hello используйте следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="2094c-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="2094c-253">Если у вас есть [установленных ураган в среде разработки](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), можно использовать следующие команды вместо hello:</span><span class="sxs-lookup"><span data-stu-id="2094c-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="2094c-254">Hello `--local` выполняется топологии hello в локальном режиме в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="2094c-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="2094c-255">Hello `-R /topology.yaml` использует hello `topology.yaml` файл ресурсов из hello jar файл toodefine hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="2094c-256">Во время их выполнения топологии hello отображает информацию о запуске.</span><span class="sxs-lookup"><span data-stu-id="2094c-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="2094c-257">После текста Hello приведен пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="2094c-258">Пакеты со сведениями журналов отправляются раз в 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2094c-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="2094c-259">Создайте копию hello `topology.yaml` файл из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="2094c-260">Имя нового файла hello `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="2094c-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="2094c-261">В hello `newtopology.yaml` файла, найдите следующую hello и измените значение hello `10` слишком`5`.</span><span class="sxs-lookup"><span data-stu-id="2094c-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="2094c-262">Этот интервал hello изменения изменения между выдача пакетов слова идет от too5 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2094c-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="2094c-263">Или, если в среде разработки имеется Storm, вы можете выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2094c-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="2094c-264">Изменение hello `/path/to/newtopology.yaml` toohello путь toohello newtopology.yaml файл, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="2094c-265">Эта команда использует hello newtopology.yaml как определения топологии hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="2094c-266">Поскольку мы не включили hello `compile` параметр Maven использует версию hello hello проекта, созданного в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="2094c-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="2094c-267">Здравствуйте, один раз запускается топологии, вы заметите, что hello время между обработкой пакетов порожденную изменила значение hello tooreflect в newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="2094c-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="2094c-268">Вы можете увидеть, можно изменить конфигурацию с помощью файла YAML без необходимости toorecompile hello топологии.</span><span class="sxs-lookup"><span data-stu-id="2094c-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="2094c-269">Дополнительные сведения об этих и других возможностях framework определен hello см. в разделе [меняется (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="2094c-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="2094c-270">Trident</span><span class="sxs-lookup"><span data-stu-id="2094c-270">Trident</span></span>

<span data-ttu-id="2094c-271">Trident — это высокоуровневая абстракция, предоставляемая Storm.</span><span class="sxs-lookup"><span data-stu-id="2094c-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="2094c-272">Он поддерживает обработку с отслеживанием состояний.</span><span class="sxs-lookup"><span data-stu-id="2094c-272">It supports stateful processing.</span></span> <span data-ttu-id="2094c-273">Основное преимущество Hello Trident — что оно гарантирует каждого сообщения, вводит топологии hello обрабатывается только один раз.</span><span class="sxs-lookup"><span data-stu-id="2094c-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="2094c-274">Без использования Trident топология только гарантирует, что каждое сообщение обрабатывается по крайней мере один раз.</span><span class="sxs-lookup"><span data-stu-id="2094c-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="2094c-275">Существуют также другие отличия, например встроенные компоненты, которые можно использовать вместо создания сит.</span><span class="sxs-lookup"><span data-stu-id="2094c-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="2094c-276">На самом деле элементы bolt заменяются не столь общими компонентами, например фильтрами, проекциями и функциями.</span><span class="sxs-lookup"><span data-stu-id="2094c-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="2094c-277">Приложения Trident можно создавать с помощью проектов Maven.</span><span class="sxs-lookup"><span data-stu-id="2094c-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="2094c-278">Использовать hello же основные шаги, представленные ранее в этой статье — только код hello отличается.</span><span class="sxs-lookup"><span data-stu-id="2094c-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="2094c-279">Trident также (в данный момент) нельзя с framework определен hello.</span><span class="sxs-lookup"><span data-stu-id="2094c-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="2094c-280">Дополнительные сведения о Trident см. в разделе hello [Обзор API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="2094c-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="2094c-281">Пример приложения Trident см. в статье [Определение популярных тем в Twitter с помощью Apache Storm в HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="2094c-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2094c-282">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2094c-282">Next Steps</span></span>

<span data-ttu-id="2094c-283">Вы узнали, как toocreate Storm топологии с помощью Java.</span><span class="sxs-lookup"><span data-stu-id="2094c-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="2094c-284">Теперь ознакомьтесь со следующими статьями.</span><span class="sxs-lookup"><span data-stu-id="2094c-284">Now learn how to:</span></span>

* [<span data-ttu-id="2094c-285">Развертывание топологий Apache Storm в HDInsight и управление ими</span><span class="sxs-lookup"><span data-stu-id="2094c-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="2094c-286">Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2094c-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="2094c-287">Другие примеры топологий Storm см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2094c-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

