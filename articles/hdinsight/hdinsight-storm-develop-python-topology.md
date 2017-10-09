---
title: "aaaApache Storm с компонентами Python - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Apache Storm топологию, которая использует компоненты Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Разработка топологий Apache Storm с помощью Python в HDInsight

Узнайте, как toocreate Apache Storm топологию, которая использует компоненты Python. Apache Storm поддерживает несколько языков, позволяет создавать вы toocombine компоненты из нескольких языков в одной топологии. Hello framework определен (впервые появилась в Storm 0.10.0) позволяет вам tooeasily создания решений, использующих компоненты Python.

> [!IMPORTANT]
> Hello сведения в этом документе была протестирована с помощью Storm на HDInsight 3.6. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Hello код для данного проекта находится в [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Предварительные требования

* Python 2.7 или выше;

* Пакет Java JDK 1.8 или более поздней версии.

* Maven 3.

* (Необязательно.) Локальная среда разработки Storm. В локальной среде Storm нужна только в том случае, если требуется топологии hello toorun локально. Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).

## <a name="storm-multi-language-support"></a>Многоязыковая поддержка Storm

Apache Storm был спроектированный toowork с компонентами, написанными на любом языке программирования. компоненты Hello необходимо понимать как toowork с hello [Thrift определение Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Для Python модуль предоставляется как часть проекта Apache Storm hello, позволяющая интерфейс tooeasily с Storm. Этот модуль можно найти по адресу [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm — это процесс Java, которое выполняется на виртуальной машине Java (JVM) hello. Компоненты, написанные на других языках, выполняются как подпроцессы. Hello Storm взаимодействует с этих вспомогательных процессов, с помощью JSON сообщений, отправляемых через стандартного ввода вывода. Дополнительные сведения о связи между компонентами, которые можно найти в hello [протокола многоязыковая](https://storm.apache.org/documentation/Multilang-protocol.html) документации.

## <a name="python-with-hello-flux-framework"></a>Python с framework определен hello

Hello меняется framework позволяет топологии Storm toodefine отдельно от компонентов hello. Hello меняется платформа использует hello Storm YAML toodefine топологии. Hello следующий текст является примером tooreference компонент Python в документе YAML hello:

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

Здравствуйте, класс `FluxShellSpout` — используется toostart hello `sentencespout.py` скрипт, который реализует hello spout.

Поток ожидает, что toobe скрипты Python hello hello `/resources` каталог внутри hello jar-файл, содержащий hello топологии. Поэтому в этом примере хранит hello сценариев Python в hello `/multilang/resources` каталога. Hello `pom.xml` включает этот файл при помощи hello следующий XML-код:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Как упоминалось ранее, имеется `storm.py` , реализующей hello определение Thrift Storm. Hello меняется framework включает в себя `storm.py` автоматически при hello сборке проекта, поэтому не нужно tooworry о ее включении.

## <a name="build-hello-project"></a>Построение проекта hello

В корневой hello hello проекта используйте hello следующую команду:

```bash
mvn clean compile package
```

Эта команда создает `target/WordCount-1.0-SNAPSHOT.jar` файл, содержащий hello компилированных топологии.

## <a name="run-hello-topology-locally"></a>Запускать локально hello топологии

Топология hello toorun локально, используйте hello следующую команду:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Для ее выполнения нужна локальная среда разработки Storm. Дополнительные сведения см. в разделе [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Настройка среды разработки).

Один раз hello топологии запускается, он создает сведения toohello локальной консоли аналогичные toohello следующий текст:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


Топология toostop hello, используйте __сочетание клавиш Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Запустите топологии Storm hello в HDInsight

1. Используйте hello следующая команда toocopy hello `WordCount-1.0-SNAPSHOT.jar` файл tooyour Storm в кластере HDInsight:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Замените `sshuser` пользователю hello SSH для кластера. Замените `mycluster` с именем кластера hello. Возможно, запрошенные tooenter hello пароль пользователя SSH hello.

    Дополнительные сведения об использовании SSH и SCP см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

2. После загрузки файла hello подключение toohello кластера с помощью SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Из сеанса SSH hello используйте следующие команды toostart hello топологии на кластере hello hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Hello пользовательского интерфейса Storm tooview hello топологии можно использовать в кластере hello. Hello Storm пользовательского интерфейса находится в https://mycluster.azurehdinsight.net/stormui. Замените `mycluster` именем кластера.

> [!NOTE]
> После запуска топология Storm выполняется до тех пор, пока она не будет остановлена. Топология hello toostop, используйте один из следующих методов hello:
>
> * Hello `storm kill TOPOLOGYNAME` команду из командной строки hello
> * Hello **Kill** кнопку в hello Storm пользовательского интерфейса.


## <a name="next-steps"></a>Дальнейшие действия

См. следующие документы для других способов toouse Python с HDInsight hello.

* [Как toouse Python для потоковой передачи задания MapReduce](hdinsight-hadoop-streaming-python.md)
* [Как toouse Python пользовательской функции (UDF) в Pig и Hive](hdinsight-python.md)
