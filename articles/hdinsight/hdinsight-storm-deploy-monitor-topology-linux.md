---
title: "aaaDeploy и управления ими Apache Storm топологии на основе Linux HDInsight | Документы Microsoft"
description: "Узнайте, как toodeploy, мониторинг и управление ими с помощью hello Storm панели мониторинга на основе Linux HDInsight топологии Apache Storm. Использование инструментов Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Развертывание топологий Apache Storm в HDInsight и управление ими

В этом документе основы hello управление и мониторинг топологии Storm, работающие на ураган в кластерах HDInsight.

> [!IMPORTANT]
> Hello шаги в этой статье, требуют Storm на основе Linux в кластере HDInsight. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Сведения о развертывании и мониторинге топологий в HDInsight под управлением Windows см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими](hdinsight-storm-deploy-monitor-topology.md).


## <a name="prerequisites"></a>Предварительные требования

* **Storm под управлением Linux в кластере HDInsight.** Инструкции по созданию кластера см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).

* (Необязательно.) **Знакомство с SSH и SCP**. Дополнительные сведения см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Необязательно) **Visual Studio**: пакет SDK Azure 2.5.1 или более поздней версии и hello Озера Data Tools для Visual Studio. Дополнительные сведения см. в статье [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Одно из следующих версий Visual Studio hello:

  * Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (любой выпуск)

  * Visual Studio 2017 (любой выпуск). В рамках hello рабочей нагрузки Azure установлены средства Озера данных для Visual Studio 2017 г.

## <a name="submit-a-topology-visual-studio"></a>Отправка топологии: Visual Studio

Средства HDInsight Hello может быть используется toosubmit C# или гибридной топологии tooyour Storm кластера. следующие шаги Hello используйте образец приложения. Сведения о создании собственных топологий с помощью средства HDInsight hello см. в разделе [топологии разработки C# с помощью hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Если вы еще не установили hello последнюю версию средств hello Озера данных для Visual Studio, в разделе [приступить к работе с помощью средств Озера данных для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hello средства Озера данных для Visual Studio ранее назывались hello средства HDInsight для Visual Studio.
    >
    > Средства Озера данных для Visual Studio включены в hello __рабочей нагрузки Azure__ для Visual Studio 2017 г.

2. Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.

3. В hello **новый проект** диалогового окна разверните **установленные** > **шаблоны**, а затем выберите **HDInsight**. Выберите из списка шаблонов hello **Storm пример**. Внизу hello диалогового окна «hello» введите имя для приложения hello.

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.

   > [!NOTE]
   > Если необходимо, введите учетные данные входа hello для подписки Azure. При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.

5. Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**. Можно отслеживать факт отправки hello выполнена с помощью hello **вывода** окна.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Отправить топологии: SSH и hello Storm команды

1. Используйте кластер HDInsight toohello tooconnect SSH. Замените **USERNAME** hello имя входа SSH. Замените **CLUSTERNAME** именем кластера HDInsight.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Дополнительные сведения об использовании SSH tooconnect tooyour HDInsight кластера см. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте следующие команды toostart пример топологии hello.

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Эта команда запускает hello пример счетчика слов топологии на кластере hello. В этой топологии случайным образом создавать предложения и число hello вхождения каждого слова в предложениях hello.

   > [!NOTE]
   > При отправке кластера toohello топологии, прежде всего необходимо скопировать файл hello JAR-файл, содержащий hello кластера перед использованием hello `storm` команды. toocopy hello toohello файлового, можно использовать hello `scp` команды. Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > Пример счетчика слов Hello и другие примеры начального уровня storm уже включены в кластере в `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Отправка топологии: программный метод

Программным путем можно развернуть tooStorm топологии на HDInsight путем взаимодействия с hello Nimbus службу, размещенную в кластере. [https://github.com/Azure-Samples/hdinsight-Java-deploy-storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) содержит пример приложения Java, демонстрирующий, как toodeploy и запуска топологии через hello Nimbus службы.

## <a name="monitor-and-manage-visual-studio"></a>Мониторинг и управление: Visual Studio

Здравствуйте, когда топологии успешно отправлена с помощью Visual Studio, **Storm топологии** просмотра отобразится hello кластера. Выберите топологию hello hello список tooview сведения о hello под управлением топологии.

![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.

Выберите фигуру hello для hello spouts или болтов tooview сведения об этих компонентах. Для каждого выбранного элемента открывается новое окно.

### <a name="deactivate-and-reactivate"></a>Деактивация и повторная активация

Деактивация топологии приостанавливает ее до завершения или повторной активации. tooperform в этих операциях используется hello __деактивировать__ и __повторно активировать__ кнопки вверху hello hello __топологии Сводка__.

### <a name="rebalance"></a>Повторная балансировка

Перераспределения топологии позволяет hello системы toorevise hello параллелизма hello топологии. Например если изменения размера кластера tooadd hello дополнительные заметки, перераспределения позволяет топологии toosee hello новых узлов.

toorebalance топологии, используйте hello __Перебалансировка__ кнопку вверху hello hello __топологии Сводка__.

> [!WARNING]
> Сначала перераспределения топологии деактивирует топология hello, затем равномерно перераспределяет работников в кластере hello, а затем наконец возвращает состояние toohello топологии hello, которое было до возникновения перераспределения. Поэтому если топологии hello был активен, он снова становится активным. Если она была отключена, то останется таковой.

### <a name="kill-a-topology"></a>Завершение работы топологии

Топологии storm продолжения, пока они не будут остановлены или hello кластер удаляется. toostop топологии, используйте hello __Kill__ кнопку вверху hello hello __топологии Сводка__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Мониторинг и управление: SSH и hello Storm команды

Hello `storm` программа позволяет toowork с работающими топологии из командной строки hello. Чтобы вывести полный список команд, воспользуйтесь `storm -h` .

### <a name="list-topologies"></a>Вывод списка топологий

Используйте hello, следующая команда toolist всех запущенных топологии:

    storm list

Эта команда возвращает сведения аналогичные toohello следующий текст:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Деактивация и повторная активация

Деактивация топологии приостанавливает ее до завершения или повторной активации. Используйте следующие команды toodeactivate hello и повторной активации:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Завершение запущенной топологии

Топологии Storm после запуска продолжают работать до тех пор, пока не будут остановлены. toostop топологии hello используйте следующую команду:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Повторная балансировка

Перераспределения топологии позволяет hello системы toorevise hello параллелизма hello топологии. Например если изменения размера кластера tooadd hello дополнительные заметки, перераспределения позволяет топологии toosee hello новых узлов.

> [!WARNING]
> Сначала перераспределения топологии деактивирует топология hello, затем равномерно перераспределяет работников в кластере hello, а затем наконец возвращает состояние toohello топологии hello, которое было до возникновения перераспределения. Поэтому если топологии hello был активен, он снова становится активным. Если она была отключена, то останется таковой.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Мониторинг и управление: пользовательский интерфейс Storm

Hello Storm пользовательского интерфейса предоставляет веб-интерфейс для работы с управлением топологии и включены в кластере HDInsight. hello tooview Storm пользовательского интерфейса, используйте браузер web tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, где **CLUSTERNAME** — hello имя кластера.

> [!NOTE]
> При получении запроса tooprovide имя пользователя и пароль, введите Здравствуйте, администратор кластера (администратор) и пароль, используемый при создании кластера hello.

### <a name="main-page"></a>Главная страница

Главная страница Hello hello Storm пользовательского интерфейса предоставляет hello следующую информацию:

* **Сводка кластера**: основные сведения о кластере Storm hello.
* **Topology summary**(Сводка по топологиям) — список запущенных топологий. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных топологии.
* **Допуск сводки**: сведения о начальника Storm hello.
* **Конфигурация nimbus**: Nimbus конфигурации для кластера hello.

### <a name="topology-summary"></a>Topology summary

При выборе ссылки из hello **топологии Сводка** разделе отображаются следующие сведения о топологии hello hello:

* **Сводка топологии**: основные сведения о топологии hello.
* **Топология действия**: операции управления, которые можно выполнять для топологии hello.

  * **Activate**(Включить) — возобновление обработки отключенной топологии.
  * **Deactivate**(Отключить) — приостановка выполняемой топологии.
  * **Перебалансировка**: корректирует параллелизм hello hello топологии. После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии. Эта операция позволяет toocompensate hello топологии tooadjust параллелизма для hello увеличивается или уменьшается число узлов в кластере hello.

    Дополнительные сведения см. в разделе <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">основные сведения о топологии Storm параллелизма hello</a>.
  * **KILL**: завершает топологии Storm после hello указано время ожидания.
* **Топология stats**: статистические данные о топологии hello. tooset Здравствуйте период времени для оставшихся записей на странице приветствия hello, используйте ссылки hello в hello **окна** столбца.
* **Spouts**: hello spouts используемой топологии hello. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных spouts.
* **Болтов**: hello винты используемой топологии hello. Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных винты.
* **Конфигурация топологии**: hello конфигурации hello выбранной топологии.

### <a name="spout-and-bolt-summary"></a>Сводка по воронкам и ситам

Выбрав spout hello **Spouts** или **болтов** разделы отображает hello следующую информацию о hello выбранного элемента:

* **Сводка компонентов**: основные сведения о hello spout или молнии.
* **Spout/молнии stats**: статистику hello spout или винта. tooset Здравствуйте период времени для оставшихся записей на странице приветствия hello, используйте ссылки hello в hello **окна** столбца.
* **Статистика ввода** (только винта): сведения о hello входные потоки, используемые hello молнии.
* **Выходные данные статистики**: сведения о потоках hello, генерируемой это spout или винта.
* **Исполнители**: сведения об экземплярах hello hello spout или молнии. Выберите hello **порт** запись для tooview определенного исполнителя, создается журнал диагностических сведений для данного экземпляра.
* **Errors**(Ошибки) — информация об ошибках для данной воронки или сита.

## <a name="monitor-and-manage-rest-api"></a>Мониторинг и управление: REST API

Hello пользовательского интерфейса Storm построено на основе hello REST API, чтобы выполнить аналогичные отслеживание и управление ими функциональные возможности с помощью API-интерфейса REST hello. Hello API-интерфейса REST toocreate пользовательские средства можно использовать для управления и мониторинга Storm топологии.

Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Hello следующие сведения являются hello конкретных toousing API REST с Apache Storm на HDInsight.

> [!IMPORTANT]
> Hello Storm REST API не является общедоступным более hello Интернета и должны быть доступны с помощью SSH туннеля toohello HDInsight головного узла кластера. Сведения о создании и использовании туннель SSH см. в разделе [использование SSH туннелирование tooaccess Ambari веб-интерфейса пользователя, диспетчер ресурсов, JobHistory, NameNode, Oozie и других сетевых интерфейсов](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>Базовый универсальный код ресурса

Hello базовый URI для hello REST API в кластерах HDInsight под управлением Linux доступна на головном узле hello в **https://HEADNODEFQDN:8744/api/v1/**. имя домена Hello hello головного узла создается во время создания кластера и не является статическим.

Можно найти hello полное доменное имя (FQDN) для головного узла кластера hello несколькими способами:

* **Из сеанса SSH**: команда hello `headnode -f` из кластера toohello сеансу SSH.
* **Из веб-Ambari**: выберите **службы** hello вверху страницы приветствия, а затем нажмите **Storm**. Из hello **Сводка** выберите **Storm пользовательского интерфейса сервера**. Hello полное доменное имя узла hello, на котором выполняется hello Storm пользовательского интерфейса и API-интерфейса REST является вверху hello страницы приветствия.
* **Из интерфейса API REST Ambari**: команда hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` ОС tooretrieve сведения об узле hello, hello Storm пользовательского интерфейса и интерфейса API REST. Замените **пароль** с hello пароль администратора для кластера hello. Замените **CLUSTERNAME** с именем кластера hello. В ответ hello запись hello «host_name» содержит hello полное доменное имя узла hello.

### <a name="authentication"></a>Аутентификация

Toohello запросы, необходимо использовать API-Интерфейс REST **обычной проверки подлинности**, поэтому использовать hello HDInsight кластер имя и пароль администратора.

> [!NOTE]
> Поскольку обычная проверка подлинности передается с помощью открытого текста, следует **всегда** использовать кластере hello toosecure подключений по протоколу HTTPS.

### <a name="return-values"></a>Возвращаемые значения

Сведения, возвращаемые из hello API-интерфейса REST только может быть одновременно доступен из кода внутри кластера hello или виртуальных машин на hello одной виртуальной сети Azure как кластер hello. Например hello полное доменное имя (FQDN), возвращаемые для серверов Zookeeper недоступна из Интернета hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как монитор и toodeploy топологии с помощью hello Storm панели мониторинга, узнайте, каким образом слишком[на языке Java, разработка топологии с помощью Maven](hdinsight-storm-develop-java-topology.md).

Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).
