---
title: "события aaaProcess из концентраторов событий с Storm - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooprocess данные из концентраторов событий Azure с топологией Storm C# создаются в Visual Studio с помощью hello средства HDInsight для Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)

Узнайте, как toowork с концентраторов событий Azure из Apache Storm на HDInsight. В этом документе используется C# Storm топологии tooread и запись данных из концентраторов Evbent

> [!NOTE]
> Этот же проект на языке Java рассматривается в статье [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

Hello в данном пошаговом руководстве используется SCP.NET пакета NuGet, который обеспечивает топологии легко toocreate C#, а также компоненты для использования с Storm на HDInsight.

> [!IMPORTANT]
> Хотя hello шагов в этом документе используют среду разработки Windows с помощью Visual Studio, hello скомпилированный проект может быть отправлено tooa Storm для кластера HDInsight, использующего Linux. Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 года.

HDInsight 3.4 и больше топологии используйте моно toorun C#. в этом документе примере Hello работает с HDInsight 3.6. Если планируется создание собственных решений .NET для HDInsight, проверьте hello [моно совместимости](http://www.mono-project.com/docs/about-mono/compatibility/) документа потенциальные проблемы совместимости.

### <a name="cluster-versioning"></a>Управление версиями кластера

Hello пакет Microsoft.SCP.Net.SDK NuGet, используемого для проекта должно соответствовать hello основной номер версии Storm установлен на HDInsight. В HDInsight версий 3.5 и 3.6 используется Storm 1.x, следовательно, для таких кластеров нужно использовать версию SCP.NET 1.0.x.x.

> [!IMPORTANT]
> пример Hello в этом документе ожидает HDInsight 3.5 или 3.6 кластера.
>
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Топологии C# должны быть рассчитаны на использование с .NET 4.5.

## <a name="how-toowork-with-event-hubs"></a>Как toowork с концентраторами событий

Корпорация Майкрософт предоставляет набор компонентов Java, которые могут быть используется toocommunicate с концентраторами событий из топологии Storm. Можно найти hello Java архива (JAR) файла, содержащего совместимой версии HDInsight 3.6 эти компоненты на [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Хотя компоненты hello написаны на языке Java, их можно легко использовать из топологии на C#.

в этом примере используются следующие компоненты Hello.

* __EventHubSpout__: считывает данные из концентраторов событий Azure;
* __EventHubBolt__: записывает данные tooEvent концентраторов.
* __EventHubSpoutConfig__: использовать tooconfigure EventHubSpout.
* __EventHubBoltConfig__: использовать tooconfigure EventHubBolt.

### <a name="example-spout-usage"></a>Пример использования объекта spout

SCP.NET предоставляет методы для добавления EventHubSpout tooyour топологии. Эти методы позволяют упростить tooadd spout, чем использование hello универсальные методы для добавления компонента Java. Hello следующем примере показано, как hello toocreate spout с помощью __SetEventHubSpout__ и **EventHubSpoutConfig** методы, предоставляемые SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

Hello предыдущего примера создается новый компонент с именем spout __EventHubSpout__и присваивает ему toocommunicate концентратора событий. Указание параллелизма Hello для компонента hello задано toohello количество разделов в концентраторе событий hello. Этот параметр позволяет Storm toocreate экземпляр компонента hello для каждой секции.

### <a name="example-bolt-usage"></a>Пример использования объекта bolt

Используйте hello **JavaComponmentConstructor** toocreate метод экземпляра hello молнии. Hello следующем примере показано, как toocreate и настройте новый экземпляр hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> В этом примере используется выражение Clojure передан в виде строки, а не с помощью **JavaComponentConstructor** toocreate **EventHubBoltConfig**, чем spout пример hello. Работает каждый из этих методов. Используйте метод hello, который, в том числе рекомендации tooyou.

## <a name="download-hello-completed-project"></a>Загрузите проект hello завершена

Можно загрузить полную версию hello проект, созданный в этом учебнике из [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Однако по-прежнему требуются параметры конфигурации tooprovide hello инструкциям в этом учебнике.

### <a name="prerequisites"></a>Предварительные требования

* [Кластер Apache Storm в HDInsight версии 3.5 или 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > пример Hello, используемые в этом документе требуется Storm в HDInsight версии 3.5 или 3.6. Это не работает с более ранними версиями HDInsight, из-за изменения имени класса toobreaking. Версию этого примера, которая работает со старыми кластерами, можно найти на сайте [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* [Концентратор событий Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).

* Hello [средства HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Пакет Java JDK 1.8 или более поздней версии, в зависимости от используемой среды разработки. Скачиваемые файлы JDK доступны на сайте [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Hello **JAVA_HOME** среды переменной должен точки toohello каталог, содержащий Java.
  * Hello **%JAVA_HOME%/bin** каталог должен находиться в пути hello.

## <a name="download-hello-event-hubs-components"></a>Загрузить компоненты hello концентраторов событий

Загрузка hello концентраторов событий spout и винта компонента из [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Создайте каталог с именем `eventhubspout`и сохраните файл hello в каталог hello.

## <a name="configure-event-hubs"></a>Настройка концентраторов событий Azure

Концентраторы событий — hello источника данных для этого примера. Используйте hello сведения в разделе «Создание концентратора событий» hello объекта [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. После создания концентратора событий hello просмотра hello **EventHub** колонки в hello Azure портала и выберите **политики общего доступа**. Выберите **+ добавить** tooadd hello следующие политики:

   | Имя | Разрешения |
   | --- | --- |
   | writer |Отправка |
   | reader |Прослушивание |

    ![Снимок экрана окна политик общего доступа](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Выберите hello **чтения** и **записи** политики. Скопируйте и сохраните hello значение первичного ключа для обоих политик, как эти значения используются в более поздней версии.

## <a name="configure-hello-eventhubwriter"></a>Настройка hello EventHubWriter

1. Если вы еще не установили hello последнюю версию средства HDInsight hello для Visual Studio, в разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Загрузите решение hello из [eventhub-storm гибридный](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. В hello **EventHubWriter** проект, откройте hello **App.config** файла. Используйте сведения hello из концентратора событий hello, настроенные ранее toofill на значение hello hello следующие ключи:

   | Ключ | Значение |
   | --- | --- |
   | EventHubPolicyName |модуль записи (Если вы использовали другое имя для политики hello с *отправки* разрешение, вместо этого используйте.) |
   | EventHubPolicyKey |Ключ политики записи hello Hello. |
   | EventHubNamespace |Здравствуйте, пространство имен, содержащее концентратора событий. |
   | EventHubName |Имя концентратора событий. |
   | EventHubPartitionCount |количество секций в концентратор событий Hello. |

4. Сохраните и закройте hello **App.config** файла.

## <a name="configure-hello-eventhubreader"></a>Настройка hello EventHubReader

1. Откройте hello **EventHubReader** проекта.

2. Откройте hello **App.config** файл для hello **EventHubReader**. Используйте сведения hello из концентратора событий hello, настроенные ранее toofill на значение hello hello следующие ключи:

   | Ключ | Значение |
   | --- | --- |
   | EventHubPolicyName |Модуль чтения (Если вы использовали другое имя для политики hello с *прослушивания* разрешение, вместо этого используйте.) |
   | EventHubPolicyKey |Ключ политики чтения hello Hello. |
   | EventHubNamespace |Здравствуйте, пространство имен, содержащее концентратора событий. |
   | EventHubName |Имя концентратора событий. |
   | EventHubPartitionCount |количество секций в концентратор событий Hello. |

3. Сохраните и закройте hello **App.config** файла.

## <a name="deploy-hello-topologies"></a>Hello топологии развертывания

1. Из **обозревателе решений**, щелкните правой кнопкой мыши hello **EventHubReader** проекта, а затем выберите **отправить tooStorm на HDInsight**.

    ![Снимок экрана обозревателя решений, с tooStorm отправить в выделенной HDInsight](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. На hello **отправить топологии** выберите ваш **кластер Storm**. Разверните **дополнительных конфигураций**выберите **пути к файлам Java**выберите **...** и выберите hello каталог, содержащий hello JAR-файл, загруженный ранее. Теперь нажмите кнопку **Отправить**.

    ![Снимок экрана с диалоговым окном Submit Topology (Отправка топологии)](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. При отправке топологии hello hello **средство просмотра топологии Storm** отображается. tooview сведения о топологии hello, выберите hello **EventHubReader** топологии hello левой панели.

    ![Снимок экрана средства просмотра топологий Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. Из **обозревателе решений**, щелкните правой кнопкой мыши hello **EventHubWriter** проекта, а затем выберите **отправить tooStorm на HDInsight**.

5. На hello **отправить топологии** выберите ваш **кластер Storm**. Разверните **дополнительных конфигураций**выберите **пути к файлам Java**выберите **...** , и выберите hello каталог, содержащий hello JAR-файл был загружен ранее. Теперь нажмите кнопку **Отправить**.

6. При отправке топологии hello обновить список топологии hello в hello **средство просмотра топологии Storm** tooverify обеих топологий, на котором работают hello кластера.

7. В **средство просмотра топологии Storm**выберите hello **EventHubReader** топологии.

8. Сводка по молнии hello компонент hello tooopen дважды щелкните hello **LogBolt** компонент на схеме hello.

9. В hello **исполнителей** выберите одну из ссылок hello в hello **порт** столбца. Отобразится информация, зарегистрированная компонентом hello. Hello в журнал сведения являются аналогичные toohello следующий текст:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Остановить hello топологии

toostop hello топологий, выберите каждой топологии в hello **средство просмотра топологии Storm**, нажмите кнопку **Kill**.

![Снимок экрана средства просмотра топологии Storm с выделенной кнопкой "Прервать"](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали, как toouse концентраторов событий Java hello spout и винта из toowork топологии C# с данными в концентраторов событий Azure. toolearn Дополнительные сведения о создании C# топологии, см. ниже hello:

* [Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Руководство по программированию для SCP](hdinsight-storm-scp-programming-guide.md)
* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)
