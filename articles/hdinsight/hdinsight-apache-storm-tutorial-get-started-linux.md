---
title: "Примеры начального уровня aaaStorm Apache Storm на HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toodo анализа больших данных и обработки данных в режиме реального времени с помощью Apache Storm и hello примеры начального уровня storm на HDInsight."
keywords: "storm-starter, пример apache storm"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Приступая к работе с Apache Storm на HDInsight с помощью примеров storm начального приветствия

Узнайте, как toouse Apache Storm в HDInsight с помощью hello примеры начального уровня storm.

Apache Storm — это масштабируемая отказоустойчивая распределенная система выполнения расчетов для обработки данных потоковой передачи в режиме реального времени. С помощью Storm вы можете создать в Azure HDInsight облачный кластер, который анализирует данные в режиме реального времени.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Знакомство с SSH и SCP**. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Создание кластера Storm

Используйте следующие шаги toocreate Storm в кластере HDInsight hello.

1. Из hello [портал Azure](https://portal.azure.com)выберите **+ создать**, **аналитики + аналитика**, а затем выберите **HDInsight**.

    ![Создание кластера HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Из hello **основы** колонке введите hello следующую информацию:

    * **Имя кластера**: hello имя кластера HDInsight hello.
    * **Подписки**: выберите toouse hello подписки.
    * **Кластер пользователя для входа** и **входа пароль кластера**: hello входа при доступе к hello кластера по протоколу HTTPS. Можно использовать эти учетные данные tooaccess службы как hello Ambari веб-интерфейса или REST API.
    * **Secure Shell (SSH) username**: hello имя входа, используемое при доступе к hello кластера через SSH. По умолчанию hello пароль является hello то же, что пароль имени входа hello кластера.
    * **Группа ресурсов**: hello ресурсов группы toocreate hello кластера.
    * **Расположение**: hello регион Azure toocreate hello кластера.

    ![Выберите подписку.](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Выберите **кластера типа**, а затем набор hello Далее значения hello **конфигурации кластера** колонки:

    * **Тип кластера**: Storm.

    * **Операционная система**: Linux.

    * **Версия**: Storm 1.1.0 (HDI 3.6).

    * **Ценовая категория кластера**: "Стандартный".

    Наконец, используйте hello **выберите** кнопку toosave параметры.

    ![Выбор типа кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. После выбора типа hello кластера использовать hello __выберите__ tooset hello кластера тип кнопки. Затем используйте hello __Далее__ кнопку toofinish базовой конфигурации.

5. Из hello **хранения** колонке выберите или создайте учетную запись хранилища. Hello в данном пошаговом руководстве оставьте hello другие поля в этой колонке в значения по умолчанию hello. Используйте hello __Далее__ кнопку toosave хранилища конфигурации.

    ![Задайте параметры учетной записи хранилища hello для HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Из hello **Сводка** колонке проверить настройку hello для hello кластера. Используйте hello __изменить__ связывает toochange все параметры, которые являются неправильными. Наконец используйте the__Create__ кнопку toocreate hello кластера.

    ![Сводка по конфигурации кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Он может занять too20 минут toocreate hello кластера.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Запуск примера storm-starter в HDInsight

1. Подключите кластер HDInsight toohello с помощью SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Если вы использовали toosecure пароль учетной записи пользователя SSH, не запрошенные tooenter его. Если используется открытый ключ, необходимо с помощью hello `-i` toospecify параметр hello соответствующим закрытым ключом. Например, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте следующие команды toostart пример топологии hello.

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > В предыдущих версиях HDInsight, имя класса hello hello топологии — `storm.starter.WordCountTopology` вместо `org.apache.storm.starter.WordCountTopology`.

    Эта команда запускает hello пример счетчика слов топологии на кластере hello, понятное имя «wordcount». Случайным образом формирует предложения и число hello вхождения каждого слова в предложениях hello.

    > [!NOTE]
    > При отправке кластеру toohello топологии, прежде всего необходимо скопировать файл hello JAR-файл, содержащий hello кластера перед использованием hello `storm` команды. Используйте hello `scp` hello toocopy командный файл. Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > Пример счетчика слов Hello и другие примеры начального уровня storm уже включены в кластере в `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Если вы заинтересованы в просмотре источника hello примеры начального уровня storm hello, можно найти код hello в [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Это ссылка для версии Storm 1.1.x, поставляемая вместе с HDInsight 3.6. Для других версий Storm использовать hello __ветви__ кнопку вверху hello tooselect страницы приветствия на другую версию Storm.

## <a name="monitor-hello-topology"></a>Монитор hello топологии

Hello Storm пользовательского интерфейса предоставляет веб-интерфейс для работы с управлением топологии и включены в кластере HDInsight.

Используйте следующие шаги toomonitor hello топологии с помощью пользовательского интерфейса Storm hello hello.

1. hello toodisplay Storm пользовательского интерфейса, откройте браузер web toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Замените **CLUSTERNAME** с hello имя кластера.

    > [!NOTE]
    > При получении запроса tooprovide имя пользователя и пароль, введите Здравствуйте, администратор кластера (администратор) и пароль, используемый при создании кластера hello.

2. В разделе **топологии Сводка**выберите hello **wordcount** запись в hello **имя** столбца. Отображается информация о топологии hello.

    ![Панель мониторинга Storm со сведениями о топологии WordCount в storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    На этой странице представлены hello следующую информацию:

    * **Топология stats** -основные сведения о производительности топологии hello, организованных в времени windows.

        > [!NOTE]
        > Выбор временного hello определенное время окна изменения окна для сведений, отображаемых в других разделах страницы приветствия.

    * **Spouts** -основные сведения о spouts, включая hello последней ошибки, возвращенный каждого spout.

    * **Bolts** (Сита) — основная информация о ситах.

    * **Конфигурация топологии** -подробные сведения о настройке топологии hello.

    Этой странице также содержатся действия, которые могут быть выполнены на hello топологии:

    * **Activate** (Включить) — возобновление обработки отключенной топологии.

    * **Deactivate** (Отключить) — приостановка выполняемой топологии.

    * **Перебалансировка** -корректирует параллелизм hello hello топологии. После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии. Перераспределения корректирует параллелизм toocompensate для hello увеличить или уменьшить количество узлов в кластере hello. Дополнительные сведения см. в разделе [основные сведения о топологии Storm параллелизма hello](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **KILL** -завершает топологии Storm после hello указано время ожидания.

3. На этой странице выберите запись из hello **Spouts** или **болтов** раздела. Отображается информация о hello выбранного компонента.

    ![Панель мониторинга Storm со сведениями о выбранных компонентах.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    На этой странице отображаются hello следующую информацию:

    * **Spout/молнии stats** -основные сведения о производительности компонента hello, организованных в времени windows.

        > [!NOTE]
        > Выбор временного hello определенное время окна изменения окна для сведений, отображаемых в других разделах страницы приветствия.

    * **Статистика ввода** (только винта) - сведения о компонентах, которые создают данные, используемые молнии hello.

    * **Output stats** (Статистика вывода) — информация о данных, созданных этим ситом.

    * **Executors** (Исполнители) — информация об экземплярах этого компонента.

    * **Errors** (Ошибки) — ошибки, созданные этим компонентом.

4. При просмотре сведений hello spout или молнии, выберите ее из hello **порт** столбца в hello **исполнителей** статьи tooview сведения для конкретного экземпляра компонента hello.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    В этом примере hello word **семь** произошла 1493957 раз. Этот счетчик представляет, сколько раз с момента запуска этой топологии произошла слово hello.

## <a name="stop-hello-topology"></a>Остановить hello топологии

Вернуть toohello **топологии Сводка** страницы для топологии hello количество слов, а затем выберите hello **Kill** кнопку hello **действия топологии** раздела. При появлении запроса введите значение 10 для hello toowait секунд перед остановкой hello топологии. По истечении периода ожидания hello топологии hello больше не отображается при посещении hello **Storm пользовательского интерфейса** hello панели мониторинга.

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Если при создании кластеров HDInsight возникли проблемы, просмотрите раздел [Access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) (Требования к контролю доступа).

## <a id="next"></a>Дальнейшие действия

В этом учебнике Apache Storm вы узнали основы работы с Storm на HDInsight hello. Далее, узнайте, как слишком[на языке Java, разработка топологии с помощью Maven](hdinsight-storm-develop-java-topology.md).

Если вы уже знакомы с разработке на языке Java топологии и toodeploy существующие tooHDInsight топологии, см. раздел [развертывание и управление ими Apache Storm топологии на HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Если вы разработчик .NET, вы можете создать топологию C# или гибридную топологию C# или Java с помощью Visual Studio. Дополнительные сведения см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Примеры топологий, которые могут использоваться с Storm на HDInsight см. следующие примеры hello.

* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
