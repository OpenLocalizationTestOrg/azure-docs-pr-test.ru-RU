---
title: "дампы кучи aaaEnable службам Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Включение дампов кучи для служб Hadoop с кластеров HDInsight, работающих под управлением Linux, для отладки и анализа."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Включение дампов кучи для служб Hadoop в HDInsight под управлением Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Файлы дампа кучи содержат снимок памяти приложения hello, включая hello значения переменных во время создания дампа hello hello. Поэтому они полезны для диагностики проблем, возникающих во время выполнения.

> [!IMPORTANT]
> Hello действия, описанные в этом документе работают только с кластерами HDInsight, использующих Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Службы

Можно включить дампы кучи для hello следующие службы:

* **Hcatalog** — tempelton;
* **Hive** — hiveserver2, metastore, derbyserver;
* **Mapreduce** — jobhistoryserver;
* **Yarn** — resourcemanager, nodemanager, timelineserver;
* **HDFS** — datanode, secondarynamenode, namenode.

Можно также включить дампы кучи для карты hello и уменьшить процессы выполнялись по HDInsight.

## <a name="configuration"></a>Основные сведения о настройке дампа кучи

Дампы памяти кучи включены путем передачи параметров (также известных как opts, или параметров) toohello виртуальной машины Java при запуске службы. Для большинства служб Hadoop службы hello оболочки скрипту toostart hello toopass могут изменять эти параметры.

В каждом сценарии является экспорта для  **\* \_OPTS**, который содержит параметры hello передан toohello виртуальной машины Java. В примере hello **hadoop env.sh** скрипта, строка hello начинается с `export HADOOP_NAMENODE_OPTS=` содержит параметры hello для hello NameNode службы.

Сопоставления и уменьшения процессы могут немного отличаться, как эти операции являются дочерний процесс hello MapReduce службы. Каждый сопоставления или уменьшите процесс выполняется в дочернем контейнере и присутствуют две записи, которые содержат параметры виртуальной машины Java hello. Оба содержатся в файле **mapred-site.xml**:

* **MapReduce.Admin.map.child.Java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> Рекомендуется с помощью Ambari hello toomodify обоих сценариев и параметры mapred-site.xml как Ambari обработки репликации изменений на узлах в кластере hello. В разделе hello [с помощью Ambari](#using-ambari) раздел конкретные действия.

### <a name="enable-heap-dumps"></a>Включение дампов кучи

Hello следующий параметр обеспечивает кучи файлы дампа при возникновении OutOfMemoryError:

    -XX:+HeapDumpOnOutOfMemoryError

Hello  **+**  указывает, что этот параметр включен. по умолчанию Hello отключено.

> [!WARNING]
> Файлы дампа кучи не включены для служб Hadoop в HDInsight по умолчанию, как файлы дампа hello могут быть большими. При включении их для устранения неполадок, помните toodisable их после воспроизвести hello проблемы и файлы дампа собрана hello.

### <a name="dump-location"></a>Расположение дампа

расположение по умолчанию Hello для файла дампа hello — hello текущий рабочий каталог. Можно выбрать, где hello файл хранится с использованием hello следующий параметр:

    -XX:HeapDumpPath=/path

Например, с помощью `-XX:HeapDumpPath=/tmp` вызывает toobe дампы hello, хранятся в каталоге/tmp hello.

### <a name="scripts"></a>Сценарии

Вы можете также запустить сценарий при возникновении ошибки **OutOfMemoryError** . Например возникла запуска уведомление, чтобы быть в курсе ошибку hello. Используйте следующие hello параметр tootrigger сценарий на __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Поскольку Hadoop распределенных систем, необходимо поместить сценарий, используемый на всех узлах в кластере hello, на котором запущена служба hello.
> 
> сценарий Hello должен также быть в расположении, которое доступно для hello hello служба выполняется как и необходимо предоставить разрешения выполнение. Например, можно назвать toostore сценариев в `/usr/local/bin` и использовать `chmod go+rx /usr/local/bin/filename.sh` toogrant разрешения read и execute.

## <a name="using-ambari"></a>Использование Ambari

toomodify hello конфигурации для службы, hello используйте следующие шаги:

1. Откройте hello Ambari web пользовательского интерфейса для кластера. URL-адрес Hello — https://YOURCLUSTERNAME.azurehdinsight.net.

    В ответ на запрос проверки подлинности toohello сайт, используя имя учетной записи hello HTTP (по умолчанию: администратора) и пароль для кластера.

   > [!NOTE]
   > Вам могут запрашиваться во второй раз, Ambari hello имя пользователя и пароль. В этом случае введите hello же имя учетной записи и пароль

2. Используя список hello hello слева, выберите область hello службы, которую необходимо toomodify. Например, **HDFS**. В центре hello установите hello **Configs** вкладки.

    ![Сеть Ambari с выбранной вкладкой конфигурации HDFS](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. С помощью hello **фильтра...**  запись, введите **opts**. Отобразятся только те элементы, в которых есть этот текст.

    ![Фильтрованный список](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Найти hello  **\* \_OPTS** tooenable обратиться в запись для службы hello tooenable дампы кучи для и добавьте параметры hello. В следующие изображения hello, я добавил `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** входа:

    ![HADOOP_NAMENODE_OPTS с -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > При включении дампы кучи для hello подключить или уменьшить дочерний процесс, найдите hello поля с именем **mapreduce.admin.map.child.java.opts** и **mapreduce.admin.reduce.child.java.opts**.

    Используйте hello **Сохранить** кнопку toosave hello изменения. Можно ввести краткое примечание, описывающее изменения hello.

5. После применения изменений hello hello **требуется перезапуск** значок отображается рядом с одной или нескольких служб.

    ![Значок «Требуется перезапуск» и кнопка «Перезапуск»](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Выберите каждую службу, которая требует перезагрузки и использовать hello **действий службы** кнопку слишком**включить в режим обслуживания**. Режим обслуживания предотвращает создание предупреждений от службы hello при повторном запуске.

    ![Включение меню режима обслуживания](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. После включения режима обслуживания, используют hello **перезапустите** кнопку для службы hello слишком**перезапустите все устаревший**

    ![Перезапустить все затронутые записи](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Здравствуйте, записи для hello **перезапустите** кнопка может быть разным для других служб.

8. После перезапуска службы hello использовать hello **действий службы** кнопку слишком**включить выключение режима обслуживания**. Это tooresume Ambari, наблюдение за оповещения для службы hello.

