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
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Запись tooHDFS из Apache Storm в HDInsight

Узнайте, как используемые Apache Storm на HDInsight toouse Storm toowrite данные toohello хранения HDFS-совместимой. HDInsight может использовать хранилище Azure и Azure Data Lake Store в качестве HDFS-совместимого хранилища. Предоставляет storm [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) компонент, который записывает tooHDFS данных. В этом документе предоставляются сведения о написании tooeither тип хранилища из hello HdfsBolt. 

> [!IMPORTANT]
> топологии, используемой в этом документе примере Hello зависит от компонентов, которые входят в состав Storm на HDInsight. Может потребоваться изменение toowork с хранилища Озера данных Azure при использовании с другими кластерами Apache Storm.

## <a name="get-hello-code"></a>Получение кода hello

Hello проекта, содержащего эту топологию можно загрузить из [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile этого проекта требуется следующая конфигурация для среды разработки hello:

* Пакет [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 1.8 или более поздней версии. Для HDInsight 3.5 или более поздней версии требуется Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки. Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.

* `JAVA_HOME`-должен указывать toohello каталог, где hello JDK установлен.
* `PATH`-должен содержать hello, следующие пути:
  
    * `JAVA_HOME`(или эквивалентный путь hello).
    * `JAVA_HOME\bin`(или эквивалентный путь hello).
    * Hello каталоге установки Maven.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Как toouse hello HdfsBolt с HDInsight

> [!IMPORTANT]
> Перед использованием hello HdfsBolt Storm на HDInsight, необходимо сначала использовать сценарии jar toocopy необходимые действия в hello `extpath` для Storm. Дополнительные сведения см. в разделе hello [настройка кластера hello](#configure) раздела.

Hello HdfsBolt использует схему файла hello, как предоставить toounderstand toowrite tooHDFS. С HDInsight используйте один из следующих схем hello.

* `wasb://` — используется с учетной записью хранения Azure.
* `adl://` — используется с Azure Data Lake Store.

Hello Следующая таблица содержит примеры использования hello файлов схемы для разных сценариев:

| Схема | Примечания |
| ----- | ----- |
| `wasb:///` | Учетная запись хранения по умолчанию Hello — это контейнер больших двоичных объектов в учетной записи хранилища Azure |
| `adl:///` | Учетная запись хранения по умолчанию Hello представляет собой каталог в хранилище Озера данных Azure. Во время создания кластера укажите каталог hello в хранилище Озера данных — основной hello HDFS hello кластера. Например, hello `/clusters/myclustername/` каталога. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Учетная запись хранилища Azure (дополнительный) не по умолчанию, связанная с hello кластера. |
| `adl://STORENAME/` | корень Hello hello hello кластере хранилища Озера данных. Эта схема позволяет tooaccess данных, расположенных за пределами hello каталог, содержащий hello кластера файловой системы. |

Дополнительные сведения см. в разделе hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) ссылку по программами.

### <a name="example-configuration"></a>Пример конфигурации

Hello следующие YAML является фрагментом hello `resources/writetohdfs.yaml` файл, включенный в пример hello. Этот файл определяет hello Storm топологии с помощью hello [определен](https://storm.apache.org/releases/1.1.0/flux.html) framework применения Apache Storm.

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

Это YAML определяет hello следующих элементов:

* `syncPolicy`: Определяет, когда файлы являются синхронизированы сброшены toohello файловой системы. В этом примере это происходит после каждой 1000 кортежей.
* `fileNameFormat`: Определяет hello путь и имя шаблона toouse при записи файлов. В этом примере путь hello предоставляется во время выполнения с помощью фильтра, и расширение файла hello `.txt`.
* `recordFormat`: Определяет hello внутренний формат файлов hello запись. В этом примере поля разделяются hello `|` символов.
* `rotationPolicy`: Определяет, когда файлы toorotate. В этом примере чередование не выполняется.
* `hdfs-bolt`: Использует hello предыдущих компонентов в качестве параметров конфигурации для hello `HdfsBolt` класса.

Дополнительные сведения о hello framework определен в разделе [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Настройка кластера hello

По умолчанию Storm на HDInsight не включает компоненты hello, что HdfsBolt использует toocommunicate с хранилища Azure или хранилища Озера данных в путь к классам Storm. Используйте hello следующий скрипт действие tooadd эти компоненты toohello `extlib` каталогом ураган в кластере:

| Скрипт URI | Узлы tooapply его | Параметры || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, руководитель | None |

Сведения об использовании этого сценария с кластером см. в разделе hello [HDInsight настроить кластеры, использующие действия скрипта](./hdinsight-hadoop-customize-cluster-linux.md) документа.

## <a name="build-and-package-hello-topology"></a>Выполните сборку и упаковку hello топологии

1. Загрузите проект пример hello из [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour среды разработки.

2. Из командной строки терминала или сеанс оболочки изменение каталоги toohello корень hello загружен проекта. toobuild и пакета hello топологии, выполните следующую команду hello.
   
        mvn compile package
   
    По завершении сборки hello и упаковка имеется новый каталог с именем `target`, которая содержит файл с именем `StormToHdfs-1.0-SNAPSHOT.jar`. Этот файл содержит топологии hello компиляции.

## <a name="deploy-and-run-hello-topology"></a>Развертывание и запуск hello топологии

1. Используйте следующие команды toocopy hello топологии toohello кластера HDInsight hello. Замените **пользователя** с именем пользователя SSH hello используется при создании кластера hello. Замените **CLUSTERNAME** с именем hello hello кластера.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    При появлении запроса введите пароль hello, используемый при создании пользователя hello SSH для hello кластера. Если открытый ключ можно использовать вместо пароля, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello сопоставления закрытый ключ.
   
   > [!NOTE]
   > Дополнительные сведения об использовании `scp` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. После завершения отправки hello используйте hello, следуя кластера HDInsight toohello tooconnect, с помощью SSH. Замените **пользователя** с именем пользователя SSH hello используется при создании кластера hello. Замените **CLUSTERNAME** с именем hello hello кластера.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    При появлении запроса введите пароль hello, используемый при создании пользователя hello SSH для hello кластера. Если открытый ключ можно использовать вместо пароля, может потребоваться toouse hello `-i` параметр toospecify hello путь toohello сопоставления закрытый ключ.
   
   Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. После подключения, используйте hello следующая команда toocreate файл с именем `dev.properties`:

        nano dev.properties

4. Используйте hello после текста как содержимое hello hello `dev.properties` файла:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > В примере предполагается, что кластер использует учетную запись хранилища Azure хранения по умолчанию hello. Если ваш кластер использует Azure Data Lake Store, используйте `hdfs.url: adl:///`.
    
    toosave hello файла, используйте __Ctrl + X__, затем __Y__и, наконец, __ввод__. Hello значения в этом файле задайте URL-адрес хранилища Озера данных hello и hello имя каталога, которые записываются данные.

3. Используйте следующие команды toostart hello топологии hello.
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Эта команда запускает hello топологии с помощью framework определен hello отправляя toohello Nimbus узел кластера hello. Топология Hello определяется hello `writetohdfs.yaml` файл, включенный в банке hello. Hello `dev.properties` файл передается в качестве фильтра, а hello значения, содержащиеся в файле hello считываются по топологии hello.

## <a name="view-output-data"></a>Просмотр выходных данных

данные tooview hello, hello используйте следующую команду:

    hdfs dfs -ls /stormdata/

Отображается список файлов hello, созданных в данной топологии.

Hello ниже приведен пример данных hello, возвращенного hello предыдущей команды.

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Остановить hello топологии

Запустите storm топологии до остановки или hello кластер удаляется. Топология hello toostop, hello используйте следующую команду:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toouse Storm toowrite tooAzure хранилище и хранилище Озера данных Azure, обнаруживать друга [Storm примеры для HDInsight](hdinsight-storm-example-topology.md).

