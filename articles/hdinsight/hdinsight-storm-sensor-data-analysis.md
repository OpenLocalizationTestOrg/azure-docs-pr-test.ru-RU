---
title: "aaaAnalyze датчиков с Apache Storm и HBase | Документы Microsoft"
description: "Узнайте, как tooconnect tooApache Storm с помощью виртуальной сети. Используйте Storm HBase tooprocess датчик данными из концентратора событий и их визуализации с D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)

Дополнительные сведения о том, как Apache Storm toouse на концентратор событий Azure данных датчика tooprocess HDInsight. Hello данных хранится в Apache HBase на HDInsight и визуализировать с помощью D3.js.

шаблон диспетчера ресурсов Azure Hello, используемый в этом документе показано, как toocreate несколько ресурсов Azure в группе ресурсов. шаблон Hello создает виртуальную сеть Azure, кластерами HDInsight (Storm и HBase) и веб-приложение Azure. Реализацию node.js на панели мониторинга реального времени является toohello автоматически развернутого веб-приложения.

> [!NOTE]
> Hello сведения в этом документе и пример в этом документе требуют HDInsight версии 3.6.
>
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Предварительные требования

* Подписка Azure.
* [Node.js](http://nodejs.org/): панель мониторинга web hello используется toopreview локально в среде разработки.
* [Java и hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): использовать toodevelop hello Storm топологии.
* [Maven](http://maven.apache.org/what-is-maven.html): hello toobuild и компиляции использованных проектов.
* [Git](http://git-scm.com/): проект hello используется toodownload из GitHub.
* **SSH** клиента: использовать кластеры HDInsight под управлением Linux toohello tooconnect. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Вам не нужен существующий кластер HDInsight. Hello в данном пошаговом руководстве создайте hello следующие ресурсы:
> 
> * виртуальная сеть Azure;
> * кластер Storm в HDInsight (под управлением Linux, с двумя рабочими узлами);
> * кластер HBase в HDInsight (под управлением Linux, с двумя рабочими узлами);
> * Веб-приложение Azure, на котором размещена панель мониторинга web hello

## <a name="architecture"></a>Архитектура

![схема архитектуры](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

В этом примере состоит из следующих компонентов hello.

* **Концентраторы событий Azure**: содержат собираемые с датчиков данные.
* **Storm в HDInsight**: в реальном времени обрабатывает данные, получаемые из концентратора событий.
* **HBase в HDInsight.**Обеспечивает постоянное хранилище данных NoSQL для данных, обработанных Storm.
* **Служба виртуальной сети Azure**: включает безопасного взаимодействия между hello Storm на HDInsight и HBase на HDInsight кластеров.
  
  > [!NOTE]
  > При использовании API клиента hello Java HBase требуется виртуальная сеть. Она не предоставляется через шлюз открытый hello для кластеров HBase. Установка HBase и Storm кластеров в одной виртуальной сети позволяет hello hello ураган кластера (или любую другую систему hello виртуальной сети) toodirectly доступ к HBase с помощью API клиента.

* **Веб-сайт панели мониторинга**: пример панели мониторинга, на которой в режиме реального времени строятся диаграммы на основе полученных данных.
  
  * веб-сайт Hello реализуется в Node.js.
  * [Socket.IO](http://socket.io/) используются для взаимодействия в режиме реального времени между топологии Storm hello и hello веб-сайта.
    
    > [!NOTE]
    > Использование Socket.io для связи относится к тонкостям реализации. На практике можно использовать любую платформу, например сокеты прямого доступа WebSocket или SignalR.

  * [D3.js](http://d3js.org/) — используется toograph hello данные, отправленные toohello веб-сайта.

> [!IMPORTANT]
> Два кластера не требуются, как не поддерживаемый метод toocreate один кластер HDInsight для Storm и HBase.

Hello топологии считывает данные из концентратора событий с помощью hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) класс и записи данных в HBase с помощью hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) класс. Связь с веб-сайта hello осуществляется с помощью [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).

Следующая схема Hello объясняется макета hello hello топологии:

![схема топологии](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Эта диаграмма представляет упрощенное представление топологии hello. Для каждого раздела концентратора событий создается экземпляр каждого компонента. Эти экземпляры будут распределены по hello узлов в кластере hello и данные передаются между ними, как показано ниже:
> 
> * Данные из средства синтаксического анализа toohello spout hello переводится подсистемой балансировки нагрузки.
> * Данные из toohello средство синтаксического анализа hello панели мониторинга и HBase группируются по Идентификатору устройства, чтобы сообщения от hello одного устройства всегда потока toohello того же компонента.

### <a name="topology-components"></a>Компоненты топологии

* **Spout концентратора событий**: hello spout входит Apache Storm версии 0.10.0 и выше.
  
  > [!NOTE]
  > Hello spout концентратора событий, используемых в этом примере требуется Storm на версия кластера HDInsight, 3.5 или 3.6.

* **ParserBolt.java**: hello данные, генерируемой hello spout необработанные JSON и иногда несколько вызывается событие за раз. Это молнии считывает данные hello, генерируемой hello spout и анализ приветственное сообщение JSON. Hello молнии затем передает данные hello как кортеж, содержащий несколько полей.
* **DashboardBolt.java**: этот компонент показано, как toouse hello Socket.io клиентская библиотека для данных toosend Java в режиме реального времени toohello панели мониторинга.
* **Нет hbase.yaml**: hello определения топологии, используемые при работе в локальном режиме. Компоненты HBase при этом не используются.
* **с hbase.yaml**: hello определения топологии, используемые при работе в кластере hello hello топологии. Компоненты HBase при этом используются.
* **dev.Properties**: hello сведения о конфигурации для концентратора событий spout hello, HBase молнии и компоненты панели мониторинга.

## <a name="prepare-your-environment"></a>Подготовка среды

Прежде чем использовать этот пример, необходимо создать концентратор событий Azure, какая топология Storm hello считывает из.

### <a name="configure-event-hub"></a>Настройка концентраторов Event Hub

Концентратор событий является hello источника данных для этого примера. Используйте следующие шаги toocreate концентратора событий hello.

1. Из hello [портал Azure](https://portal.azure.com)выберите **+ создать** -> **Интернета вещей** -> **концентраторов событий**.
2. В hello **создать пространство имен** выполните hello следующие задачи:
   
   1. Введите **имя** для hello пространства имен.
   2. Выберите ценовую категорию. **Базовый** подойдет для этого примера.
   3. Выберите hello Azure **подписки** toouse.
   4. Создайте группу ресурсов или выберите имеющуюся.
   5. Выберите hello **расположение** для hello концентратора событий.
   6. Выберите **toodashboard ПИН-код**, а затем нажмите кнопку **создать**.

3. После завершения процесса создания hello отображается hello сведения концентраторов событий для пространства имен. В этой колонке выберите **+ Add Event Hub**(+ Добавить концентратор событий). В hello **создать концентратор событий** статьи, введите имя **sensordata**, а затем выберите **создать**. Оставьте остальные поля в значения по умолчанию hello hello.
4. Из концентраторов событий hello просмотра пространства имен, выберите **концентраторов событий**. Выберите hello **sensordata** входа.
5. Hello sensordata концентратора событий, выберите **политики общего доступа**. Используйте hello **+ добавить** следующими политиками hello tooadd ссылку:

    | Имя политики | Claims |
    | ----- | ----- |
    | устройства | Отправка |
    | storm | Прослушивание |

1. Выберите обе политики и запишите hello **ПЕРВИЧНОГО ключа** значение. Необходимо получить значение hello для обеих политик на следующих этапах.

## <a name="download-and-configure-hello-project"></a>Загрузить и настроить проект hello

Используйте следующую toodownload hello проекта из GitHub hello.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

После выполнения команды hello имеется hello следующая структура каталогов:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> В этом документе не рассматривается в сведениях о toofull включены в этом примере кода hello. Тем не менее полностью закомментирована кода hello.

tooread проекта hello tooconfigure из концентратора событий, откройте hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` и добавьте ваш toohello сведения концентратора событий, следующие строки:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Локальная компиляция и тестирование

> [!IMPORTANT]
> Использование топологии hello локально требует рабочий Storm среды разработки. См. дополнительные сведения о [настройке среды разработки Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) на сайте Apache.org.

> [!WARNING]
> При использовании среды разработки Windows может появиться `java.io.IOException` при выполнении топологии hello локально. В этом случае перемещение по топологии hello toorunning на HDInsight.

Перед началом тестирования, необходимо запустить hello мониторинга tooview hello выходные данные топологии hello и создать toostore данные в концентратор событий.

> [!IMPORTANT]
> При тестировании локально компонент HBase Hello этой топологии не активен. Hello API-интерфейса Java для hello HBase кластера нельзя получить доступ из внешней hello виртуальной сети Azure, содержащей hello кластеров.

### <a name="start-hello-web-application"></a>Запуск веб-приложения hello

1. Откройте командную строку и перейдите в каталог слишком`hdinsight-eventhub-example/dashboard`. Используйте следующие команды tooinstall hello зависимости, необходимые веб-приложением hello hello.
   
    ```bash
    npm install
    ```

2. Используйте следующие команды toostart hello веб-приложение hello.
   
    ```bash
    node server.js
    ```
   
    Вы видите toohello аналогичные сообщения после текста:
   
        Server listening at port 3000

3. Откройте веб-браузер и введите `http://localhost:3000/` в качестве адреса hello. Отображается примерно toohello страницы, после изображения.
   
    ![веб-панель мониторинга](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Не закрывайте окно командной строки. После тестирования, используйте сочетание клавиш Ctrl-C toostop hello веб-сервера.

### <a name="generate-data"></a>Создание данных

> [!NOTE]
> Hello действия, описанные в этом разделе используют Node.js, чтобы их можно использовать на любой платформе. Другие примеры языка в разделе hello `SendEvents` каталога.

1. Открыть новую строку, оболочки или терминала и перейдите слишком`hdinsight-eventhub-example/SendEvents/nodejs`. tooinstall hello зависимости, необходимые для приложения hello, hello используйте следующую команду:

    ```bash
    npm install
    ```

2. Привет открыть `app.js` в текстовом редакторе и добавьте hello полученного ранее сведения концентратора событий:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > В этом примере предполагается, что используется `sensordata` имени hello концентратора событий. И что `devices` имени hello hello политика, имеющая `Send` утверждения.

3. Используйте hello следующая команда tooinsert новых записей в концентратор событий:
   
    ```bash
    node app.js
    ```
   
    Вы увидите, что несколько строк выходных данных, содержащих данные hello отправлено tooEvent концентратора:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Построения и запуска топологии hello

1. Откройте новую командную строку и перейдите в каталог слишком`hdinsight-eventhub-example/TemperatureMonitor`. toobuild и пакета hello топологии, выполните следующую команду hello. 

    ```bash
    mvn clean package
    ```

2. Топология toostart hello в локальном режиме hello используйте следующую команду:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`запускает топологии hello в локальном режиме.
    * `--filter`использует hello `dev.properties` файл toopopulate параметров в определении топологии hello.
    * `resources/no-hbase.yaml`использует hello `no-hbase.yaml` определения топологии.
 
   После запуска топологии hello считывает записи из концентратора событий и отправляет их toohello панели мониторинга, запущенного на локальном компьютере. Вы увидите строки отображаются в hello панели мониторинга, аналогичную toohello после изображения:
   
    ![панель мониторинга с данными](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Во время hello панели мониторинга с помощью hello `node app.js` команда из предыдущего hello шаги toosend новых данных tooEvent концентраторов. Поскольку значения температуры hello случайным образом создаются, граф hello следует обновить tooshow значительные изменения в температуры.
   
   > [!NOTE]
   > Вы должны находиться в hello **hdinsight-eventhub пример/SendEvents/Nodejs** каталог при использовании hello `node app.js` команды.

3. После проверки этой панели мониторинга hello обновляет топологии hello stop, с помощью клавиш Ctrl + C. Также можно использовать сочетание клавиш Ctrl + C toostop hello локальный веб-сервер.

## <a name="create-a-storm-and-hbase-cluster"></a>Создание кластеров Storm и HBase

Hello шаги этого раздела используется [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate виртуальной сети Azure и Storm и HBase кластера hello виртуальной сети. шаблон Hello также создает веб-приложение Azure и развертывает копию hello панели мониторинга в него.

> [!NOTE]
> Виртуальная сеть используется, чтобы топологии hello, работающих в кластере Storm hello может напрямую взаимодействовать с hello HBase кластера с помощью API-интерфейса Java HBase hello.

Hello шаблона диспетчера ресурсов, используемых в данном документе, расположенные в контейнере большой двоичный объект открытого в **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Щелкните hello toosign кнопки в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Из hello **развертывания пользовательского** введите hello следующие значения:
   
    ![Параметры HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Базовые имена кластеров**: это значение используется как базовое имя hello для кластеров hello Storm и HBase. Например, если ввести **abc**, будут созданы кластер Storm **storm-abc** и кластер HBase **hbase-abc**.
   * **Имя входа пользователя кластера**: hello имя пользователя администратора для кластеров hello Storm и HBase.
   * **Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Storm и HBase hello.
   * **Имя пользователя SSH**: hello toocreate пользователя SSH для кластеров hello Storm и HBase.
   * **Пароль SSH**: hello пароль пользователя SSH hello для кластеров hello Storm и HBase.
   * **Расположение**: hello области создания кластеров hello в.
     
     Нажмите кнопку **ОК** toosave hello параметров.

3. Используйте hello **основы** статьи toocreate группу ресурсов или выберите существующий.
4. В hello **расположение группы ресурсов** раскрывающееся меню, выберите hello местоположения, которые вы выбрали для hello **расположение** параметр в hello **параметры** раздела.
5. Прочитайте hello положения и условия, а затем выберите **я принимаю условия, указанных выше, toohello**.
6. Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**. Занимает около 20 минут toocreate hello кластеров.

После создания ресурсов hello отображается информация о группе ресурсов hello.

![Группа ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ storm** и **базовое имя hbase**, где базовое имя — имя hello указано toohello шаблона. Эти имена на более позднем этапе используется при подключении toohello кластеров. Также Обратите внимание, что hello имя узла мониторинга hello — **мониторинга базовым именем**. Это значение используется ниже в этом документе.

## <a name="configure-hello-dashboard-bolt"></a>Настройка мониторинга молнии hello

мониторинга данных toohello toosend развернуто как веб-приложения, необходимо изменить hello, следующей строкой в hello `dev.properties`файла:

```yaml
dashboard.uri: http://localhost:3000
```

Изменение `http://localhost:3000` слишком`http://BASENAME-dashboard.azurewebsites.net` и сохраните файл hello. Замените **базовым ИМЕНЕМ** с базовым именем hello, указанное в предыдущем шаге hello. Можно также использовать hello группы ресурсов, созданные ранее tooselect hello панели мониторинга и представления hello URL-адрес.

## <a name="create-hello-hbase-table"></a>Создайте таблицу HBase hello

toostore данных в HBase, необходимо сначала создать таблицу. Предварительно создать ресурсы, необходимые для Storm toowrite для, как идет ресурсы toocreate внутри топологии Storm может привести к попытке несколько экземпляров toocreate hello того же ресурса. Создать hello ресурсам за пределами топологии hello и использовать Storm для чтения/записи и аналитики.

1. Используйте SSH tooconnect toohello HBase кластера с помощью hello SSH пользователя и пароль, указанный шаблон toohello во время создания кластера. Например, при соединении с помощью hello `ssh` используется hello, используя синтаксис команды:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Замените `sshuser` с имя пользователя SSH hello заданы при создании кластера hello. Замените `clustername` с именем кластера HBase hello.

2. Из сеанса SSH hello запустите оболочку HBase hello.
   
    ```bash
    hbase shell
    ```
   
    После загрузки оболочки hello, вы видите `hbase(main):001:0>` строки.

3. Введите следующая команда toocreate датчиков таблицы toostore hello hello hello оболочки HBase:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Убедитесь, что для этой таблицы hello был создан с помощью hello следующую команду:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Возвращает сведения аналогичные toohello следующий пример, об отсутствии 0 строк в таблице hello.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Введите `exit` tooexit hello оболочки HBase:

## <a name="configure-hello-hbase-bolt"></a>Настройка молнии HBase hello

tooHBase toowrite из кластера Storm hello, необходимо предоставить hello HBase молнии hello сведения о конфигурации кластера HBase.

1. Используйте один из следующих примеров tooretrieve hello Zookeeper кворума для кластера HBase hello.

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Замените `your_HDInsight_cluster_name` с hello имя кластера HDInsight. Дополнительные сведения об установке hello `jq` программы, в разделе [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > При появлении запроса введите пароль hello для входа администратора HDInsight hello.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Замените "your_HDInsight_cluster_name с hello имя кластера HDInsight. При появлении запроса введите пароль hello для входа администратора HDInsight hello.
    >
    > Для этого примера требуется Azure PowerShell. См. дополнительные сведения об [установке Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).

    Hello информацию, возвращаемую эти примеры — примерно toohello следующий текст:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Эта информация используется toocommunicate Storm с кластером HBase hello.

2. Изменение hello `dev.properties` и добавьте hello Zookeeper кворума сведения toohello следующей строкой:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Построение пакета и разверните решение tooHDInsight hello

В среде разработки используйте следующие шаги toodeploy hello Storm топологии toohello storm кластера hello.

1. Из hello `TemperatureMonitor` каталога, используйте hello следующую команду tooperform новую сборку и создать пакет JAR-ФАЙЛ из проекта:
   
        mvn clean package
   
    Эта команда создает файл с именем `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` в целевом каталоге проекта.

2. Использование scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` и `dev.properties` кластер Storm tooyour файлов. Следующий пример, замените в hello `sshuser` с пользователем SSH hello, указанный при создании кластера hello и `clustername` с именем hello Storm кластера. При появлении запроса введите пароль hello для hello пользователя SSH.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Он может занять несколько минут tooupload hello файлы.

    Дополнительные сведения об использовании hello `scp` и `ssh` команд с HDInsight, в разделе [использование SSH с HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. После загрузки файла hello подключите кластер Storm toohello, с помощью SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Замените `sshuser` с именем пользователя SSH hello. Замените `clustername` с имя_кластера Storm hello.

4. toostart hello топологии, выполните следующую команду из сеанса SSH hello hello.
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`отправляет toohello топологии hello Nimbus службу, которая распространяет его toohello начальника узлы кластера hello.
    * `--filter`использует hello `dev.properties` файл toopopulate параметров в определении топологии hello.
    * `-R /with-hbase.yaml`использует hello `with-hbase.yaml` топологии, включенный в пакет hello.

5. После запуска топологии hello, откройте веб-сайт toohello браузера, опубликованных в Azure, а затем используйте hello `node app.js` команда toosend данных tooEvent концентратора. Вы увидите информацию о hello toodisplay обновление в панели мониторинга веб hello.
   
    !["Веб-транзакции"](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Просмотр данных HBase

Используйте следующие шаги tooconnect tooHBase hello и убедитесь, что hello записи данных toohello таблицы:

1. Использование SSH tooconnect toohello HBase кластера.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Замените `sshuser` с именем пользователя SSH hello. Замените `clustername` с именем кластера HBase hello.

2. Из сеанса SSH hello запустите оболочку HBase hello.
   
    ```bash
    hbase shell
    ```
   
    После загрузки оболочки hello, вы видите `hbase(main):001:0>` строки.

3. Представление строк из таблицы hello:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Эта команда возвращает сведения аналогичные toohello после текста, указывающее на данные в таблице hello.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Эта операция сканирования возвращает максимум 10 строк из таблицы hello.

## <a name="delete-your-clusters"></a>Удаление кластеров

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello кластеров, хранения и веб-приложения за один раз удаления группы ресурсов hello, содержащий их.

## <a name="next-steps"></a>Дальнейшие действия

Другие примеры топологий Storm с HDInsight приведены в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).

Дополнительные сведения о Apache Storm см. в разделе hello [Apache Storm](https://storm.incubator.apache.org/) сайта.

Дополнительные сведения о HBase на HDInsight см. в разделе hello [HBase с HDInsight Обзор](hdinsight-hbase-overview.md).

Дополнительные сведения о Socket.io см. в разделе hello [socket.io](http://socket.io/) сайта.

Дополнительные сведения о D3.js см. на странице [D3.js - Data Driven Documents](http://d3js.org/) (D3.js. Документы, управляемые данными).

Сведения о создании топологий на языке Java см. в статье [Разработка топологий на основе Java для базовых приложений подсчета слов с помощью Apache Storm и Maven в HDInsight](hdinsight-storm-develop-java-topology.md).

Сведения о создании топологий на .NET см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
