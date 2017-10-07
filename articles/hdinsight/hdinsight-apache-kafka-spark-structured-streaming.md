---
title: "Spark структурированных потоковой передачи с Kafka - Azure HDInsight aaaApache | Документы Microsoft"
description: "Узнайте, как toouse Apache Spark потоковой передачи (DStream) tooget данных в таблицу или из Apache Kafka. В этом примере показано, как выполнить потоковую передачу данных, используя записную книжку Jupyter из Spark в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Использование структурированной потоковой передачи Spark с Kafka (предварительная версия) в HDInsight

Узнайте, как toouse Spark структурированных потоковой передачи данных tooread из Kafka Apache на Azure HDInsight.

Структурированная потоковая передача Spark — это механизм обработки потока, встроенный в Spark SQL. Он позволяет вам вычисления потоковой передачи tooexpress hello то же, что вычисление пакета со статическими данными. Дополнительные сведения о структурированной потоковой передачи. в разделе hello [структурированных потоковой передачи руководство по программированию [альфа]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) с программами.

> [!IMPORTANT]
> В этом примере используется Spark 2.1 в HDInsight 3.6. Структурированная потоковая передача рассматривается как __альфа-версия__ в Spark 2.1.
>
> Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Spark в HDInsight и Kafka в кластере HDInsight. Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластера Spark взаимодействовать с hello Kafka кластера.
>
> После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.

## <a name="create-hello-clusters"></a>Создавать кластеры hello

Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello. Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера. В этом примере hello Kafka и Spark кластеры расположены в виртуальной сети Azure. Hello следующей схеме показаны связи потоки между кластерами hello:

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Hello Kafka службы — ограниченный toocommunication в виртуальной сети hello. Другие службы в кластере hello, такие как SSH и Ambari, могут быть доступны через hello Интернета. Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Вы можете создать виртуальную сеть Azure, Kafka и Spark кластеров вручную, это упрощает toouse шаблона диспетчера ресурсов Azure. Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Spark кластеры tooyour подписки Azure.

1. Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Этот шаблон создает hello следующие ресурсы:

    * Kafka в кластере HDInsight 3.5;
    * Spark в кластере HDInsight 3.6;
    * Виртуальная сеть Azure, содержащий hello кластеров HDInsight.

    > [!IMPORTANT]
    > Hello структурированных потоковой передачи записной книжки используются в этом примере требуется Spark в HDInsight 3.6. При использовании более ранней версии Spark на HDInsight, возникнут ошибки при использовании записной книжки hello.

2. После записи hello toopopulate сведений на hello hello используйте **развертывания пользовательского** колонки:
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую. Эта группа содержит кластер HDInsight hello.

    * **Расположение**: выберите расположение территориально закрыть tooyou.

    * **Базовые имена кластеров**: это значение используется как базовое имя hello для hello Spark и Kafka кластеров. Например, если ввести **hdi**, будет создан кластер Spark с именем spark-hdi__ и кластер Kafka с именем **kafka-hdi**.

    * **Имя входа пользователя кластера**: hello имя пользователя администратора для hello Spark и Kafka кластеров.

    * **Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Spark и Kafka hello.

    * **Имя пользователя SSH**: hello toocreate пользователя SSH для hello Spark и Kafka кластеров.

    * **Пароль SSH**: hello пароль пользователя SSH hello для hello Spark и Kafka кластеров.

3. Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.

4. Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**. Занимает около 20 минут toocreate hello кластеров.

После создания ресурсов hello предпринимается колонки группы ресурсов перенаправленный toohello.

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ spark** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона. Использовать эти имена на последующих этапах при подключении toohello кластеров.

## <a name="get-hello-kafka-brokers"></a>Получить hello Kafka брокеров

Hello кода в этом примере подключается toohello Kafka компонента service broker узлов в кластере Kafka hello. toofind hello Kafka узлов брокера, выполните следующий пример PowerShell или Bash hello.

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> В этом примере ожидает `$PASSWORD` toocontain hello пароль для имени входа кластера hello, и `$CLUSTERNAME` toocontain имя hello hello Kafka кластера.
>
> В этом примере используется hello [jq](https://stedolan.github.io/jq/) программа tooparse данных из документа JSON hello.

Hello выходных данных аналогичные toohello следующий текст:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Сохраните эти сведения, так как он используется в следующих разделах данного документа hello.

## <a name="get-hello-notebooks"></a>Получить записных книжек hello

Hello код для примера hello, описанные в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Отправка записных книжек hello

Используйте следующую записных книжек hello tooupload действия из проекта hello tooyour Spark в кластере HDInsight hello.

1. В веб-браузере подключитесь записной книжки Jupyter toohello на свой кластер Spark. В hello URL-адреса, замените `CLUSTERNAME` с именем hello Kafka кластера:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    При появлении запроса введите hello кластера входа (для администратора) и пароль, используемый при создании кластера hello.

2. Hello верхней правой части страницы приветствия, с помощью hello __отправить__ hello tooupload кнопку __поток-Твиты-To_Kafka.ipynb__ файл toohello кластера. Выберите __откройте__ toostart hello передачи.

    ![Использовать tooselect кнопка отправки hello и отправка записной книжке](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Выберите файл KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Найти hello __поток-Твиты-To_Kafka.ipynb__ запись в списке hello портативные компьютеры, а затем выберите __отправить__ кнопку рядом с ней.

    ![Используйте hello передачи рядом hello KafkaStreaming.ipynb входа tooupload его toohello записной книжки сервера](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Повторите шаги 1 – 3 hello tooload __Spark-структурированный-потоковой передачи-в-Kafka.ipynb__ ноутбука.

## <a name="load-tweets-into-kafka"></a>Загрузка твитов в Kafka

После загрузки файлов hello выберите hello __поток-Твиты-To_Kafka.ipynb__ записной книжки hello tooopen входа. Выполните действия hello hello записной книжки tooload твиты в Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Обработка твитов с помощью структурированной потоковой передачи

Hello книжке Jupyter домашнюю страницу, выберите hello __Spark-структурированный-потоковой передачи-в-Kafka.ipynb__ входа. Выполните действия hello hello записной книжки tooload твиты из Kafka, с помощью потоковой передачи структурированных Spark.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toouse Spark структурированных потоковой передачи, см. следующие дополнительные сведения о работе с Spark и Kafka toolearn документы hello:

* [Как toouse усилить потоковой передачи (DStream) с Kafka](hdinsight-apache-spark-with-kafka.md).
* [Начало работы с записной книжкой Jupyter и Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).