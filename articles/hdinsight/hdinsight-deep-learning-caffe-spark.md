---
title: "aaaUse Caffe на Azure HDInsight Spark для распределенных углубленного обучения | Документы Microsoft"
description: "Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения


## <a name="introduction"></a>Введение

Углубленного обучения влияет все данные из сферы здравоохранения tootransportation toomanufacturing и многое другое. Компании требуется включить toodeep обучения toosolve сложных проблем, таких как [изображения классификации](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [распознавания речи](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)объекта распознавания и машинного перевода. 

Существует [множество популярных платформ](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), в том числе [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano и т. д. Caffe является одним из hello самый знаменитый платформы не являющиеся символьными (императивного) нейронной сети и широко используется во многих областях, включая компьютерного зрения. Более того, система [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) сочетает в себе возможности Caffe и Apache Spark, за счет чего глубокое обучение может выполняться непосредственно в кластере Hadoop с конвейерами извлечения, преобразования и загрузки Spark. Это уменьшает сложность системы комплексного обучения и задержки при выполнении этого процесса.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) — hello только предложения Hadoop полностью управляются облака, предоставляющий оптимизированный аналитической кластеров открытым исходным кодом для Spark, Hive, MapReduce, HBase, Storm, Kafka и R Server, поддерживаемый 99,9% SLA. Каждую из этих технологий работы с большими данными и каждое из этих приложений от независимых поставщиков программного обеспечения можно с легкостью развернуть в качестве управляемого кластера, обеспечив при этом безопасность и мониторинг корпоративного класса.

Некоторые пользователи просим нам о том, как toouse глубокого изучения на HDInsight PaaS Hadoop продуктов корпорации Майкрософт. Мы должны иметь дополнительные tooshare в будущем hello, однако сегодня мы хотим toosummarize Технический блог о том, как toouse Caffe на HDInsight Spark.

Если вы устанавливали Caffe раньше, вы заметили, что этот процесс связан с определенными трудностями. В этом блоге мы будет показано как tooinstall [Caffe на Spark](https://github.com/yahoo/CaffeOnSpark) для кластера HDInsight, затем использовать hello встроенных MNIST Демонстрация toodemostrate как toouse распределенных углубленного обучения с помощью HDInsight Spark на процессорах.

Существует четыре основных шагов tooget, он работает в HDInsight.

1. Установите необходимые hello зависимости на всех узлах hello
2. Построение Caffe на Spark для HDInsight на головном узле hello
3. Распространение hello необходимые библиотеки tooall hello рабочих узлов
4. Разработка модели и распределенный запуск Caffe.

Так как HDInsight решением PaaS, он обеспечивает значительные функций - это довольно просто tooperform некоторые задачи. Одна из функций hello, активно используемые в этой записи блога называется [действие сценария](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), с которой выполнен оболочки команды toocustomize узлов кластера (головного узла, рабочий узел или граничного узла).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Шаг 1: Установка hello необходимые зависимости на всех узлах hello

tooget к работе, нам нужна tooinstall hello зависимости, которые необходимы. узел Caffe Hello и [CaffeOnSpark сайта](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) предлагает некоторые вики-сайте очень полезен для установки зависимостей hello для Spark на YARN режиме (режим hello для HDInsight Spark), но нам нужен tooadd несколько Дополнительные зависимости для платформы HDInsight. Мы будет используйте действие скрипта hello, как показано ниже и запустите его на всех узлах головного hello и узлов рабочих ролей. Его выполнение занимает примерно 20 минут, так как эти зависимости также зависят от других пакетов. Необходимо поместить его в нужное расположение, доступный tooyour кластера HDInsight, такие как расположение GitHub или учетной записи хранилища больших двоичных ОБЪЕКТОВ по умолчанию hello.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Действие сценария hello выше состоит из двух этапов. Hello первым шагом является tooinstall Здравствуйте, все необходимые библиотеки. Эти библиотеки включают в себя необходимые библиотеки hello для компиляции Caffe (например, gflags glog) и на которых работает Caffe (например, numpy). Мы используем libatlas оптимизации использования ЦП, но может всегда следуют за hello CaffeOnSpark wiki об установке других библиотек оптимизации, например MKL или CUDA (для GPU).

Hello второй шаг — toodownload, скомпилировать и установить protobuf 2.5.0 для Caffe во время выполнения. Protobuf 2.5.0 [требуется](https://github.com/yahoo/CaffeOnSpark/issues/87), однако эта версия не предоставляется в виде пакета на Ubuntu 16, поэтому мы должны toocompile его из исходного кода hello. Есть несколько ресурсов на hello Интернет о том, как toocompile, такие как [это](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply начать работу, просто выполните это действие сценария для вашей рабочей hello tooall кластера узлов, узлов и head (для HDInsight 3.5). Можно либо запустить hello действий сценария для выполнения кластера или hello действия скрипта можно также запустить во время подготовки кластера hello. Дополнительные сведения о действиях скрипта hello см. в разделе документации hello [здесь](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Действия сценария tooInstall зависимости](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Шаг 2: Построение Caffe на Spark для HDInsight на головном узле hello

второй шаг Hello — toobuild Caffe на hello головному узлу, а затем распространите hello скомпилированные библиотеки tooall hello рабочих узлов. На этом шаге необходимо будет слишком[ssh в к головному узлу](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), просто выполните hello [процесс построения CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), а ниже приведен скрипт hello toobuild CaffeOnSpark можно использовать ряд дополнительных действий. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Может потребоваться toodo больше, чем говорит документации CaffeOnSpark какие hello. Hello изменениям относятся:
- Изменение только tooCPU и использование libatlas для этой конкретной цели.
- Поместите hello наборы данных toohello BLOB-ОБЪЕКТА хранилища, которое является общей папкой, доступный tooall рабочих узлов для последующего использования.
- PUT hello скомпилированных Caffe библиотеки tooBLOB хранилища, а позже будет копировать с помощью дополнительных компиляции действия сценария tooavoid этих библиотек tooall hello узлов.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Устранение неполадок, связанных с ошибкой An Ant BuildException has occured: exec returned: 2

При первом toobuild CaffeOnSpark иногда появится сообщение

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Репозиторий кода просто чистой hello, «создание чистой», а затем выполнения» убедитесь построения» решает эту проблему, поскольку имеют правильные зависимости hello.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Устранение неполадок, связанных с ошибкой времени ожидания подключения к репозиторию Maven

Иногда maven дает мне ошибка времени ожидания подключения hello, аналогичные toobelow:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Оно ОК после ожидания в течение нескольких минут и затем повторите toorebuild hello кода, поэтому он может быть Maven каким-либо образом ограничения hello трафик от данного IP-адреса.


### <a name="troubleshooting-test-failure-for-caffe"></a>Устранение неполадок, связанных со сбоем тестирования Caffe

Возможно, появится сбоя теста при выполнении hello окончательная проверка для CaffeOnSpark, аналогичные с ниже. Это prabably, связанные с кодировкой UTF-8, но не должен влиять hello использование Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Шаг 3: Распространять hello необходимые библиотеки tooall hello рабочих узлов

Hello следующим шагом является toodistribute hello библиотеки (по сути hello библиотек в CaffeOnSpark/caffe-public или распространять/lib/и CaffeOnSpark/caffe автомат или распространять/lib /) tooall hello узлов. На шаге 2 мы поместили эти библиотеки в хранилище больших двоичных ОБЪЕКТОВ, и на этом шаге мы используем скрипт действия toocopy его tooall hello головного узла и узлов рабочих ролей.

toodo, простого выполнения сценария действия, как показано ниже (требуется правильное местоположение конкретного tooyour toopoint toohello кластера):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Так как на шаге 2 мы поместили в хранилище больших двоичных ОБЪЕКТОВ, т. е узлы hello доступного tooall hello, на этом шаге мы просто скопировать tooall hello узлов.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Этап 4. Разработка модели и распределенный запуск Caffe

После выполнения hello выше действия, который, установлены на головному узлу hello уже Caffe и мы являются хорошим toogo. Hello следующим шагом является toowrite Caffe модели. 

Caffe использует «выразительный архитектура,» там, где для составления модель, точно так же, вы должны toodefine файл конфигурации, а также без создания кода (в большинстве случаев). Давайте рассмотрим этот процесс более подробно. 

Сегодня мы обучить модель Hello является образца модели для обучения MNIST. База данных MNIST Hello рукописные цифр имеет 60 000 примеров обучающий и проверочный набор из 10 000 примеров. Это подмножество более широкого набора из базы данных NIST. Hello цифр были нормализованы размер и по центру в образе фиксированного размера. CaffeOnSpark имеет некоторые сценарии toodownload hello dataset и преобразовать его в нужном формате hello.

Эта система предоставляет несколько образцов сетевых топологий для обучения MNIST. Он имеет четкий разработки разделения hello сетевую архитектуру (hello топологии сети hello) и оптимизации. В этом случае вам потребуется два указанных ниже файла. 

файл «Поиск решения» Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) используется для наблюдения за hello оптимизации и создания параметра обновления. Например, определяет ли ЦП или GPU будет использован, какова импульс hello, число итераций, будут выполняться, и т. д. Он также определяет топологию сети нейрон следует Здравствуйте, используйте программу (который является второй файл hello будут). Дополнительные сведения о поиска решения можно найти слишком[Caffe документации](http://caffe.berkeleyvision.org/tutorial/solver.html).

Например так как мы используем ЦП, а не GPU, мы следует изменить hello последней строки для:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

При необходимости вы можете изменить и другие строки.

второй файл Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) определяет как сети нейрон hello выглядит и соответствующих входных данных hello и выходного файла. Мы также должны tooupdate hello tooreflect hello обучающих данных местоположения. Изменение hello следующие части в lenet_memory_train_test.prototxt (требуется правильное местоположение конкретного tooyour toopoint toohello кластера).

- изменить file:/Users/mridul/bigml/demodl/mnist_train_lmdb «hello» слишком "wasb: / / / проекты/machine_learning/image_dataset/mnist_train_lmdb»
- Измените «file:/Users/mridul/bigml/demodl/mnist_test_lmdb/» слишком "wasb: / / / проекты/machine_learning/image_dataset/mnist_test_lmdb»

![Конфигурация Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Дополнительные сведения о как toodefine hello сети Проверьте hello [Caffe документацию по MNIST набора данных](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Целью этого блога hello мы просто используйте этот простой пример MNIST. Hello указанную ниже команду необходимо запускать из головного узла hello.

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

По сути он распределяет hello необходимые файлы (lenet_memory_solver.prototxt и lenet_memory_train_test.prototxt) tooeach YARN контейнера, а также задать hello соответствующие пути каждого tooLD_LIBRARY_PATH драйвера или исполнитель Spark, которая определена в hello предыдущего фрагмента и точки toohello расположения в коде с CaffeOnSpark библиотеки. 

## <a name="monitoring-and-troubleshooting"></a>Мониторинг и устранение неполадок

Так как мы используем режим YARN кластера, в этом случае драйвер Spark hello будет запланированных tooan произвольный контейнер (и произвольные рабочий узел) вы должны видеть только в вывод консоли hello что-то наподобие:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Если вы хотите tooknow, что произошло, обычно требуется журнал tooget hello Spark драйвер, который содержит дополнительные сведения. В этом случае необходимо toogo toohello пользовательского интерфейса YARN toofind hello YARN журналы. Чтобы узнать hello YARN пользовательского интерфейса, этот URL-адрес: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Пользовательский интерфейс YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Здесь вы можете просмотреть сведения о количестве выделенных ресурсов для этого конкретного приложения. Можно щелкнуть ссылку «Планировщик» hello, и будет отображаться для этого приложения, 9 запущенных контейнеров. Мы просим YARN tooprovide 8 исполнителей, а другой контейнер — для процесса драйвера. 

![Планировщик YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Вы можете toocheck hello драйвер журналов или контейнер журналов в случае сбоев. Для журналов драйвера можно щелкните идентификатор приложения hello в пользовательском Интерфейсе YARN, а затем нажмите кнопку «Журналы» hello. Hello драйвер журналы записываются в stderr.

![Пользовательский интерфейс YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Например может появиться некоторые hello следующую ошибку из журналов драйвер hello, о том, что выделено слишком много исполнителей.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

В некоторых случаях hello проблема может произойти на исполнителей, а не драйверы. В этом случае необходимо toocheck hello контейнера журналы. Всегда получать журналы контейнера hello и затем получить hello сбой контейнер. Например, этот сбой может произойти при запуске Caffe.

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

В этом случае требуется идентификатор контейнера hello сбой tooget (hello выше случая при container_1485916338528_0008_05_000005). Затем необходимо toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

из головному узлу hello. вы определите, что он произошел из-за использования режима графического процессора в файле lenet_memory_solver.prototxt (вместо режима ЦП).

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Получение результатов

Поскольку мы выделяемый 8 исполнителей и топология сети hello проста, его обычно занимает около 30 минут toorun hello результат. Из командной строки hello, вы увидите мы поместить toowasb:///mnist.model модели hello и помещать hello результаты tooa папку с именем wasb: / / / mnist_features_result.

Hello результаты можно получить, выполнив

    hadoop fs -cat hdfs:///mnist_features_result/*

и как выглядит результат hello:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Hello SampleID представляет идентификатор hello в наборе данных MNIST hello и hello метки является определяет число hello, hello модели.


## <a name="conclusion"></a>Заключение

В этой документации предпринята tooinstall CaffeOnSpark с работающими простой пример. HDInsight — это платформа распределенных вычислений полный управляемой облачной и hello лучше всего подходит для выполнения машинного обучения и расширенных аналитических рабочих нагрузок на большой набор данных, и для распределенной углубленного обучения, можно использовать Caffe на HDInsight Spark tooperform углубленного обучения задачи.


## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

