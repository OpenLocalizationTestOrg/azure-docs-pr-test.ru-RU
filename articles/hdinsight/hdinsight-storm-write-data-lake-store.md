---
title: "Запись данных Apache Storm в хранилище Azure или Data Lake Store для Azure HDInsight | Документация Майкрософт"
description: "Сведения об использовании Apache Storm для записи данных в HDFS-совместимое хранилище для HDInsight. Хранилище Azure или Azure Data Lake Store предоставляет HDFS-совместимое хранилище для HDInsight. В этом документе и связанном примере демонстрируется, как компонент HdfsBolt можно использовать для записи в хранилище Storm по умолчанию в кластере HDInsight."
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="64060-105">Запись данных в HDFS из Apache Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="64060-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="64060-106">Узнайте об использовании Storm для записи данных в HDFS-совместимое хранилище, используемое Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64060-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="64060-107">HDInsight может использовать хранилище Azure и Azure Data Lake Store в качестве HDFS-совместимого хранилища.</span><span class="sxs-lookup"><span data-stu-id="64060-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="64060-108">Storm предоставляет компонент [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html), который записывает данные в HDFS.</span><span class="sxs-lookup"><span data-stu-id="64060-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="64060-109">В этой статье предоставляются сведения о записи данных в хранилища обоих типов из HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="64060-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="64060-110">Пример топологии, используемый в этом документе, зависит от компонентов, которые входят в состав Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64060-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="64060-111">Может потребоваться изменить его для работы с Azure Data Lake Store при использовании с другими кластерами Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="64060-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="64060-112">Получение кода</span><span class="sxs-lookup"><span data-stu-id="64060-112">Get the code</span></span>

<span data-ttu-id="64060-113">Проект, содержащий эту топологию, можно скачать на странице [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="64060-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="64060-114">Чтобы скомпилировать этот проект, требуется следующая конфигурация среды разработки:</span><span class="sxs-lookup"><span data-stu-id="64060-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="64060-115">Пакет [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="64060-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="64060-116">Для HDInsight 3.5 или более поздней версии требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="64060-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="64060-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="64060-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="64060-118">Во время установки Java и JDK на компьютере, где ведется разработка, могут быть установлены следующие переменные среды.</span><span class="sxs-lookup"><span data-stu-id="64060-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="64060-119">Однако следует убедиться, что они существуют и что они содержат правильные значения для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="64060-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="64060-120">`JAVA_HOME`. Эта переменная должна указывать на каталог, в который установлен JDK.</span><span class="sxs-lookup"><span data-stu-id="64060-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="64060-121">`PATH`. Эта переменная должна содержать следующие пути:</span><span class="sxs-lookup"><span data-stu-id="64060-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="64060-122">`JAVA_HOME` или эквивалентный путь.</span><span class="sxs-lookup"><span data-stu-id="64060-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="64060-123">`JAVA_HOME\bin` или эквивалентный путь.</span><span class="sxs-lookup"><span data-stu-id="64060-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="64060-124">Каталог, в который установлено ПО Maven.</span><span class="sxs-lookup"><span data-stu-id="64060-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="64060-125">Как использовать HdfsBolt с HDInsight</span><span class="sxs-lookup"><span data-stu-id="64060-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64060-126">Перед использованием HdfsBolt Storm в HDInsight необходимо выполнить действие скрипта, чтобы скопировать необходимые JAR-файлы в `extpath` для Storm.</span><span class="sxs-lookup"><span data-stu-id="64060-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="64060-127">Дополнительные сведения см. в статье [Использование Azure Data Lake Store с помощью Apache Storm в HDInsight (Java)](#configure).</span><span class="sxs-lookup"><span data-stu-id="64060-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="64060-128">HdfsBolt использует предоставленную схему файла, чтобы понять, как выполнять запись данных в HDFS.</span><span class="sxs-lookup"><span data-stu-id="64060-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="64060-129">Для HDInsight используйте одну из следующих схем:</span><span class="sxs-lookup"><span data-stu-id="64060-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="64060-130">`wasb://` — используется с учетной записью хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="64060-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="64060-131">`adl://` — используется с Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64060-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="64060-132">Следующая таблица содержит примеры использования схемы файлов для разных сценариев.</span><span class="sxs-lookup"><span data-stu-id="64060-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="64060-133">Схема</span><span class="sxs-lookup"><span data-stu-id="64060-133">Scheme</span></span> | <span data-ttu-id="64060-134">Примечания</span><span class="sxs-lookup"><span data-stu-id="64060-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="64060-135">Учетная запись хранения по умолчанию — это контейнер больших двоичных объектов в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="64060-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="64060-136">Учетная запись хранения по умолчанию представляет собой каталог в Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64060-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="64060-137">Во время создания кластера укажите каталог в Data Lake Store, который является корнем системы HDFS кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="64060-138">Например, каталог `/clusters/myclustername/`.</span><span class="sxs-lookup"><span data-stu-id="64060-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="64060-139">Учетная запись хранения Azure не по умолчанию (дополнительная), связанная с кластером.</span><span class="sxs-lookup"><span data-stu-id="64060-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="64060-140">Корень Data Lake Store, используемый кластером.</span><span class="sxs-lookup"><span data-stu-id="64060-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="64060-141">Эта схема позволяет получить доступ к данным, размещенным вне каталога, в котором содержится файловая система кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="64060-142">Дополнительные сведения см. в [справочнике HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) на сайте Apache.org.</span><span class="sxs-lookup"><span data-stu-id="64060-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="64060-143">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="64060-143">Example configuration</span></span>

<span data-ttu-id="64060-144">Следующий YAML-файл является фрагментом файла `resources/writetohdfs.yaml`, который включен в пример.</span><span class="sxs-lookup"><span data-stu-id="64060-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="64060-145">Этот файл определяет топологию Storm с помощью платформы [Flux](https://storm.apache.org/releases/1.1.0/flux.html) для Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="64060-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="64060-146">Это YAML-файл определяет следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="64060-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="64060-147">`syncPolicy` — определяет, когда файлы синхронизируются или записываются в файловую систему.</span><span class="sxs-lookup"><span data-stu-id="64060-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="64060-148">В этом примере это происходит после каждой 1000 кортежей.</span><span class="sxs-lookup"><span data-stu-id="64060-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="64060-149">`fileNameFormat` — определяет шаблон пути и имени файла, используемый при записи файлов.</span><span class="sxs-lookup"><span data-stu-id="64060-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="64060-150">В этом примере путь предоставляется во время выполнения с помощью фильтра, а файл имеет расширение `.txt`.</span><span class="sxs-lookup"><span data-stu-id="64060-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="64060-151">`recordFormat` — определяет внутренний формат записанных файлов.</span><span class="sxs-lookup"><span data-stu-id="64060-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="64060-152">В этом примере поля разделяются с помощью символа `|`.</span><span class="sxs-lookup"><span data-stu-id="64060-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="64060-153">`rotationPolicy` — определяет, когда чередуются файлы.</span><span class="sxs-lookup"><span data-stu-id="64060-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="64060-154">В этом примере чередование не выполняется.</span><span class="sxs-lookup"><span data-stu-id="64060-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="64060-155">`hdfs-bolt` — использует предыдущие компоненты в качестве параметров конфигурации для класса `HdfsBolt`.</span><span class="sxs-lookup"><span data-stu-id="64060-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="64060-156">Дополнительные сведения о платформе Flux см. на странице [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="64060-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="64060-157">Настройка кластера</span><span class="sxs-lookup"><span data-stu-id="64060-157">Configure the cluster</span></span>

<span data-ttu-id="64060-158">По умолчанию Storm в HDInsight не содержит компоненты, которые HdfsBolt использует для взаимодействия с хранилищем Azure или Data Lake Store в пути к классу Storm.</span><span class="sxs-lookup"><span data-stu-id="64060-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="64060-159">Используйте следующее действие скрипта, чтобы добавить эти компоненты в каталог `extlib` для Storm в кластере:</span><span class="sxs-lookup"><span data-stu-id="64060-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="64060-160">| URI скрипта | узлы, к которым нужно применить | параметры | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | узлы Nimbus, Supervisor | None |</span><span class="sxs-lookup"><span data-stu-id="64060-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="64060-161">Сведения об использовании этого скрипта с кластером см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](./hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="64060-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="64060-162">Сборка и упаковка топологии</span><span class="sxs-lookup"><span data-stu-id="64060-162">Build and package the topology</span></span>

1. <span data-ttu-id="64060-163">Скачайте пример проекта на странице [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) в среду разработки.</span><span class="sxs-lookup"><span data-stu-id="64060-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="64060-164">С помощью командной строки, терминала или сеанса работы с оболочкой измените каталоги на корень загруженного проекта.</span><span class="sxs-lookup"><span data-stu-id="64060-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="64060-165">Для сборки и создания пакета топологии выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64060-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="64060-166">По завершении сборки и упаковки будет создан каталог `target`, который содержит файл `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="64060-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="64060-167">Этот файл содержит скомпилированную топологию.</span><span class="sxs-lookup"><span data-stu-id="64060-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="64060-168">Развертывание и запуск топологии</span><span class="sxs-lookup"><span data-stu-id="64060-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="64060-169">Для копирования топологии в кластер HDInsight воспользуйтесь следующей командой.</span><span class="sxs-lookup"><span data-stu-id="64060-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="64060-170">Замените **USER** именем пользователя SSH, используемым при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="64060-171">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="64060-172">При появлении запроса введите пароль, который применялся при создании пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="64060-173">Если вместо пароля используется открытый ключ, может потребоваться использовать параметр `-i` и указать путь к соответствующему закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="64060-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="64060-174">Дополнительные сведения об использовании `scp` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64060-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="64060-175">После завершения отправки используйте следующую команду для подключения к кластеру HDInsight с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="64060-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="64060-176">Замените **USER** именем пользователя SSH, используемым при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="64060-177">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="64060-178">При появлении запроса введите пароль, который применялся при создании пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="64060-179">Если вместо пароля используется открытый ключ, может потребоваться использовать параметр `-i` и указать путь к соответствующему закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="64060-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="64060-180">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64060-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="64060-181">После подключения создайте файл `dev.properties` с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="64060-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="64060-182">Добавьте в файл `dev.properties` следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="64060-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="64060-183">В этом примере предполагается, что кластер использует учетную запись хранения Azure в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64060-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="64060-184">Если ваш кластер использует Azure Data Lake Store, используйте `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="64060-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="64060-185">Чтобы сохранить этот файл, нажмите клавиши __CTRL+X__, введите __Y__ и нажмите клавишу __ВВОД__.</span><span class="sxs-lookup"><span data-stu-id="64060-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="64060-186">Значения в этом файле позволяют задать URL-адрес Data Lake Store и имя каталога, в который записываются данные.</span><span class="sxs-lookup"><span data-stu-id="64060-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="64060-187">Запустите топологию, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="64060-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="64060-188">Эта команда запускает топологию с помощью платформы Flux и отправляет ее в узел Nimbus кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="64060-189">Топология определяется в файле `writetohdfs.yaml`, включенном в JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="64060-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="64060-190">Файл `dev.properties` передается в качестве фильтра, и топология считывает содержащиеся в нем значения.</span><span class="sxs-lookup"><span data-stu-id="64060-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="64060-191">Просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="64060-191">View output data</span></span>

<span data-ttu-id="64060-192">Для просмотра данных используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="64060-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="64060-193">Отобразится список файлов, созданных с помощью этой топологии.</span><span class="sxs-lookup"><span data-stu-id="64060-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="64060-194">Ниже приведен пример списка, возвращаемого предыдущими командами.</span><span class="sxs-lookup"><span data-stu-id="64060-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="64060-195">Остановка топологии</span><span class="sxs-lookup"><span data-stu-id="64060-195">Stop the topology</span></span>

<span data-ttu-id="64060-196">Топологии Storm будут выполняться до остановки или удаления кластера.</span><span class="sxs-lookup"><span data-stu-id="64060-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="64060-197">Для остановки топологии введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64060-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="64060-198">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="64060-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="64060-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64060-199">Next steps</span></span>

<span data-ttu-id="64060-200">Теперь, когда вы узнали, как применять Storm для записи в хранилище Azure и Azure Data Lake Store, изучите другие [примеры Storm для HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="64060-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

