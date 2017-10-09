---
title: "aaaApache Storm записи tooStorage/данных Озера хранилища - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello Apache Storm toowrite toohello HDFS-совместимой хранилища для HDInsight. Azure хранилища или хранилища Озера данных Azure обеспечивают хранение hello HDFS comptabile HDInsight. В этом документе и связанные примере hello демонстрируется компонент HdfsBolt hello хранения по умолчанию используется toowrite toohello Storm в кластере HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="0410b-105">Запись tooHDFS из Apache Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0410b-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="0410b-106">Узнайте, как используемые Apache Storm на HDInsight toouse Storm toowrite данные toohello хранения HDFS-совместимой.</span><span class="sxs-lookup"><span data-stu-id="0410b-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="0410b-107">HDInsight может использовать хранилище Azure и Azure Data Lake Store в качестве HDFS-совместимого хранилища.</span><span class="sxs-lookup"><span data-stu-id="0410b-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="0410b-108">Предоставляет storm [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) компонент, который записывает tooHDFS данных.</span><span class="sxs-lookup"><span data-stu-id="0410b-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="0410b-109">В этом документе предоставляются сведения о написании tooeither тип хранилища из hello HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="0410b-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0410b-110">топологии, используемой в этом документе примере Hello зависит от компонентов, которые входят в состав Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0410b-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="0410b-111">Может потребоваться изменение toowork с хранилища Озера данных Azure при использовании с другими кластерами Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0410b-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="0410b-112">Получение кода hello</span><span class="sxs-lookup"><span data-stu-id="0410b-112">Get hello code</span></span>

<span data-ttu-id="0410b-113">Hello проекта, содержащего эту топологию можно загрузить из [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="0410b-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="0410b-114">toocompile этого проекта требуется следующая конфигурация для среды разработки hello:</span><span class="sxs-lookup"><span data-stu-id="0410b-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="0410b-115">Пакет [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0410b-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="0410b-116">Для HDInsight 3.5 или более поздней версии требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="0410b-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="0410b-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="0410b-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="0410b-118">Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки.</span><span class="sxs-lookup"><span data-stu-id="0410b-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="0410b-119">Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="0410b-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="0410b-120">`JAVA_HOME`-должен указывать toohello каталог, где hello JDK установлен.</span><span class="sxs-lookup"><span data-stu-id="0410b-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="0410b-121">`PATH`-должен содержать hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="0410b-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="0410b-122">`JAVA_HOME`(или эквивалентный путь hello).</span><span class="sxs-lookup"><span data-stu-id="0410b-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="0410b-123">`JAVA_HOME\bin`(или эквивалентный путь hello).</span><span class="sxs-lookup"><span data-stu-id="0410b-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="0410b-124">Hello каталоге установки Maven.</span><span class="sxs-lookup"><span data-stu-id="0410b-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="0410b-125">Как toouse hello HdfsBolt с HDInsight</span><span class="sxs-lookup"><span data-stu-id="0410b-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0410b-126">Перед использованием hello HdfsBolt Storm на HDInsight, необходимо сначала использовать сценарии jar toocopy необходимые действия в hello `extpath` для Storm.</span><span class="sxs-lookup"><span data-stu-id="0410b-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="0410b-127">Дополнительные сведения см. в разделе hello [настройка кластера hello](#configure) раздела.</span><span class="sxs-lookup"><span data-stu-id="0410b-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="0410b-128">Hello HdfsBolt использует схему файла hello, как предоставить toounderstand toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="0410b-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="0410b-129">С HDInsight используйте один из следующих схем hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="0410b-130">`wasb://` — используется с учетной записью хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="0410b-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="0410b-131">`adl://` — используется с Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0410b-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="0410b-132">Hello Следующая таблица содержит примеры использования hello файлов схемы для разных сценариев:</span><span class="sxs-lookup"><span data-stu-id="0410b-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="0410b-133">Схема</span><span class="sxs-lookup"><span data-stu-id="0410b-133">Scheme</span></span> | <span data-ttu-id="0410b-134">Примечания</span><span class="sxs-lookup"><span data-stu-id="0410b-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="0410b-135">Учетная запись хранения по умолчанию Hello — это контейнер больших двоичных объектов в учетной записи хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="0410b-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="0410b-136">Учетная запись хранения по умолчанию Hello представляет собой каталог в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0410b-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="0410b-137">Во время создания кластера укажите каталог hello в хранилище Озера данных — основной hello HDFS hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="0410b-138">Например, hello `/clusters/myclustername/` каталога.</span><span class="sxs-lookup"><span data-stu-id="0410b-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="0410b-139">Учетная запись хранилища Azure (дополнительный) не по умолчанию, связанная с hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="0410b-140">корень Hello hello hello кластере хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="0410b-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="0410b-141">Эта схема позволяет tooaccess данных, расположенных за пределами hello каталог, содержащий hello кластера файловой системы.</span><span class="sxs-lookup"><span data-stu-id="0410b-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="0410b-142">Дополнительные сведения см. в разделе hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) ссылку по программами.</span><span class="sxs-lookup"><span data-stu-id="0410b-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="0410b-143">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="0410b-143">Example configuration</span></span>

<span data-ttu-id="0410b-144">Hello следующие YAML является фрагментом hello `resources/writetohdfs.yaml` файл, включенный в пример hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="0410b-145">Этот файл определяет hello Storm топологии с помощью hello [определен](https://storm.apache.org/releases/1.1.0/flux.html) framework применения Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="0410b-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="0410b-146">Это YAML определяет hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0410b-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="0410b-147">`syncPolicy`: Определяет, когда файлы являются синхронизированы сброшены toohello файловой системы.</span><span class="sxs-lookup"><span data-stu-id="0410b-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="0410b-148">В этом примере это происходит после каждой 1000 кортежей.</span><span class="sxs-lookup"><span data-stu-id="0410b-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="0410b-149">`fileNameFormat`: Определяет hello путь и имя шаблона toouse при записи файлов.</span><span class="sxs-lookup"><span data-stu-id="0410b-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="0410b-150">В этом примере путь hello предоставляется во время выполнения с помощью фильтра, и расширение файла hello `.txt`.</span><span class="sxs-lookup"><span data-stu-id="0410b-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="0410b-151">`recordFormat`: Определяет hello внутренний формат файлов hello запись.</span><span class="sxs-lookup"><span data-stu-id="0410b-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="0410b-152">В этом примере поля разделяются hello `|` символов.</span><span class="sxs-lookup"><span data-stu-id="0410b-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="0410b-153">`rotationPolicy`: Определяет, когда файлы toorotate.</span><span class="sxs-lookup"><span data-stu-id="0410b-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="0410b-154">В этом примере чередование не выполняется.</span><span class="sxs-lookup"><span data-stu-id="0410b-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="0410b-155">`hdfs-bolt`: Использует hello предыдущих компонентов в качестве параметров конфигурации для hello `HdfsBolt` класса.</span><span class="sxs-lookup"><span data-stu-id="0410b-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="0410b-156">Дополнительные сведения о hello framework определен в разделе [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="0410b-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="0410b-157">Настройка кластера hello</span><span class="sxs-lookup"><span data-stu-id="0410b-157">Configure hello cluster</span></span>

<span data-ttu-id="0410b-158">По умолчанию Storm на HDInsight не включает компоненты hello, что HdfsBolt использует toocommunicate с хранилища Azure или хранилища Озера данных в путь к классам Storm.</span><span class="sxs-lookup"><span data-stu-id="0410b-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="0410b-159">Используйте hello следующий скрипт действие tooadd эти компоненты toohello `extlib` каталогом ураган в кластере:</span><span class="sxs-lookup"><span data-stu-id="0410b-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="0410b-160">| Скрипт URI | Узлы tooapply его | Параметры || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, руководитель | None |</span><span class="sxs-lookup"><span data-stu-id="0410b-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="0410b-161">Сведения об использовании этого сценария с кластером см. в разделе hello [HDInsight настроить кластеры, использующие действия скрипта](./hdinsight-hadoop-customize-cluster-linux.md) документа.</span><span class="sxs-lookup"><span data-stu-id="0410b-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="0410b-162">Выполните сборку и упаковку hello топологии</span><span class="sxs-lookup"><span data-stu-id="0410b-162">Build and package hello topology</span></span>

1. <span data-ttu-id="0410b-163">Загрузите проект пример hello из [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour среды разработки.</span><span class="sxs-lookup"><span data-stu-id="0410b-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="0410b-164">Из командной строки терминала или сеанс оболочки изменение каталоги toohello корень hello загружен проекта.</span><span class="sxs-lookup"><span data-stu-id="0410b-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="0410b-165">toobuild и пакета hello топологии, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="0410b-166">По завершении сборки hello и упаковка имеется новый каталог с именем `target`, которая содержит файл с именем `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="0410b-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="0410b-167">Этот файл содержит топологии hello компиляции.</span><span class="sxs-lookup"><span data-stu-id="0410b-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="0410b-168">Развертывание и запуск hello топологии</span><span class="sxs-lookup"><span data-stu-id="0410b-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="0410b-169">Используйте следующие команды toocopy hello топологии toohello кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="0410b-170">Замените **пользователя** с именем пользователя SSH hello используется при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="0410b-171">Замените **CLUSTERNAME** с именем hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="0410b-172">При появлении запроса введите пароль hello, используемый при создании пользователя hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="0410b-173">Если открытый ключ можно использовать вместо пароля, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello сопоставления закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="0410b-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0410b-174">Дополнительные сведения об использовании `scp` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0410b-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0410b-175">После завершения отправки hello используйте hello, следуя кластера HDInsight toohello tooconnect, с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="0410b-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="0410b-176">Замените **пользователя** с именем пользователя SSH hello используется при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="0410b-177">Замените **CLUSTERNAME** с именем hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="0410b-178">При появлении запроса введите пароль hello, используемый при создании пользователя hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0410b-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="0410b-179">Если открытый ключ можно использовать вместо пароля, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello сопоставления закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="0410b-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="0410b-180">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0410b-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="0410b-181">После подключения, используйте hello следующая команда toocreate файл с именем `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="0410b-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="0410b-182">Используйте hello после текста как содержимое hello hello `dev.properties` файла:</span><span class="sxs-lookup"><span data-stu-id="0410b-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="0410b-183">В примере предполагается, что кластер использует учетную запись хранилища Azure хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="0410b-184">Если ваш кластер использует Azure Data Lake Store, используйте `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="0410b-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="0410b-185">toosave hello файла, используйте __Ctrl + X__, затем __Y__и, наконец, __ввод__.</span><span class="sxs-lookup"><span data-stu-id="0410b-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="0410b-186">Hello значения в этом файле задайте URL-адрес хранилища Озера данных hello и hello имя каталога, которые записываются данные.</span><span class="sxs-lookup"><span data-stu-id="0410b-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="0410b-187">Используйте следующие команды toostart hello топологии hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="0410b-188">Эта команда запускает hello топологии с помощью framework определен hello отправляя toohello Nimbus узел кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="0410b-189">Топология Hello определяется hello `writetohdfs.yaml` файл, включенный в банке hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="0410b-190">Hello `dev.properties` файл передается в качестве фильтра, а hello значения, содержащиеся в файле hello считываются по топологии hello.</span><span class="sxs-lookup"><span data-stu-id="0410b-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="0410b-191">Просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="0410b-191">View output data</span></span>

<span data-ttu-id="0410b-192">данные tooview hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0410b-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="0410b-193">Отображается список файлов hello, созданных в данной топологии.</span><span class="sxs-lookup"><span data-stu-id="0410b-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="0410b-194">Hello ниже приведен пример данных hello, возвращенного hello предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="0410b-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="0410b-195">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="0410b-195">Stop hello topology</span></span>

<span data-ttu-id="0410b-196">Запустите storm топологии до остановки или hello кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="0410b-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="0410b-197">Топология hello toostop, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0410b-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="0410b-198">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="0410b-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="0410b-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0410b-199">Next steps</span></span>

<span data-ttu-id="0410b-200">Теперь, когда вы узнали, как toouse Storm toowrite tooAzure хранилище и хранилище Озера данных Azure, обнаруживать друга [Storm примеры для HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0410b-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

