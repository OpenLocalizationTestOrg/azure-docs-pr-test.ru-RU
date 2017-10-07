---
title: "aaaApache Spark потоковой передачи с Kafka - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse данных toostream Spark Apache Spark в или из него с помощью DStreams Kafka Apache. В этом примере показано, как выполнить потоковую передачу данных, используя записную книжку Jupyter из Spark в HDInsight."
keywords: "пример kafka, kafka zookeeper, потоковая передача spark kafka, пример потоковой передачи spark kafka"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Пример потоковой передачи Apache Spark (DStream) с использованием Kafka (предварительная версия) в HDInsight

Узнайте, как toouse данных toostream Spark Apache Spark в или из Kafka Apache на HDInsight с помощью DStreams. В этом примере используется записной книжке Jupyter, который выполняется на кластере Spark hello.
> [!NOTE]
> Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Spark в HDInsight и Kafka в кластере HDInsight. Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластера Spark взаимодействовать с hello Kafka кластера.
>
> После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.

## <a name="create-hello-clusters"></a>Создавать кластеры hello

Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello. Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера. В этом примере hello Kafka и Spark кластеры расположены в виртуальной сети Azure. Hello следующей схеме показаны связи потоки между кластерами hello:

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> То, что Kafka себя ограниченный toocommunication в виртуальной сети hello, другие службы в кластере hello такие, как можно получить через SSH и Ambari hello Интернета. Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Вы можете создать виртуальную сеть Azure, Kafka и Spark кластеров вручную, это упрощает toouse шаблона диспетчера ресурсов Azure. Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Spark кластеры tooyour подписки Azure.

1. Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов. Этот шаблон создает кластер Kafka, содержащий три рабочих узла.

    Этот шаблон создает кластер HDInsight 3.6 для Kafka и Spark.

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

После создания ресурсов hello предпринимается колонке перенаправленный tooa hello группы ресурсов, содержащий кластеров hello и панели мониторинга.

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ spark** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона. Использовать эти имена на последующих этапах при подключении toohello кластеров.

## <a name="use-hello-notebooks"></a>С помощью ноутбуков hello

Hello код для примера hello, описанные в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Следуйте указаниям hello hello `README.md` файл toocomplete в этом примере.

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure. Удаление группы hello удаляет все ресурсы, созданные после этого документа, hello виртуальной сети Azure и учетной записи хранения, используемые в кластерах hello.

## <a name="next-steps"></a>Дальнейшие действия

В этом примере вы узнали, как toouse усилить tooread и записи tooKafka. Используйте следующие ссылки toodiscover hello других способов toowork с Kafka:

* [Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))
* [Используйте MirrorMaker toocreate реплику Kafka в HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight](hdinsight-apache-storm-with-kafka.md)

