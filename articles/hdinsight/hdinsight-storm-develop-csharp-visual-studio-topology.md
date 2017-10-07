---
title: "aaaApache Storm топологии с Visual Studio и C# - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Storm топологии на C#. Создайте топологию количество простых word в Visual Studio с помощью средств hello Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Разрабатывать приложения топологии на C# с помощью средств hello Озера данных для Visual Studio для Apache Storm

Узнайте, как toocreate топологии Storm C# с помощью Озера данных Azure hello (Hadoop) tools для Visual Studio. В этом документе рассматриваются hello процесс создания Storm проекта в Visual Studio, локального тестирования и развертывания tooan Apache Storm на кластере Azure HDInsight.

Вы также узнаете, как toocreate гибридной топологии, использующих компоненты C# и Java.

> [!NOTE]
> Хотя hello в данном пошаговом руководстве зависят от среды разработки Windows с помощью Visual Studio, hello скомпилированный проект может быть отправлено tooeither кластера HDInsight под управлением Windows или Linux. Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 года.

Топология toouse C# в кластере под управлением Linux, необходимо обновить hello пакет Microsoft.SCP.Net.SDK NuGet, используемый в ваш проект tooversion 0.10.0.6 или более поздней версии. Hello версию пакета hello должно также совпадать hello основной номер версии Storm установлен на HDInsight.

| Версия HDInsight | Версия Storm | Версия SCP.NET | Версия Mono по умолчанию |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(только в HDInsight под управлением Windows) | Нет данных |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C# топологиях для кластеров под управлением Linux необходимо использовать .NET 4.5 и использовать моно toorun hello кластера HDInsight. Чтобы определить потенциальные проблемы с совместимостью, просмотрите документ о [совместимости Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="install-visual-studio"></a>Установка Visual Studio

C# топологии с SCP.NET можно разрабатывать с помощью одного из следующих версий Visual Studio hello:

* Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 или [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (любой выпуск)

## <a name="install-data-lake-tools-for-visual-studio"></a>Установка средств Data Lake для Visual Studio

tooinstall Озера данных средства для Visual Studio, выполните действия hello в [приступить к работе с помощью средств Озера данных для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Установка Java

При отправке топологии Storm из Visual Studio, SCP.NET создает ZIP-файл, содержащий топологии hello и зависимости. Java — используется toocreate эти ZIP-файлы, так как он использует формат, который является более совместимым с кластеров на основе Linux.

1. Установите hello Java Developer Kit (JDK) 7 или более поздней версии среды разработки. Вы можете получить hello Oracle JDK из [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Вы также можете использовать [другие дистрибутивы Java](http://openjdk.java.net/).

2. Hello `JAVA_HOME` среды переменной должен точки toohello каталог, содержащий Java.

3. Hello `PATH` переменной среды должен включать hello `%JAVA_HOME%\bin` каталога.

Можно использовать следующие C# консольного приложения tooverify правильность установки Java и hello JDK hello.

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Шаблоны Storm

средства Озера данных Hello для Visual Studio предоставляют hello следующие шаблоны:

| Тип проекта | Что демонстрирует |
| --- | --- |
| Приложение Storm |Пустой проект топологии Storm |
| Пример модуля записи Storm Azure SQL |Как toowrite tooAzure базы данных SQL. |
| Пример модуля чтения Storm Azure Cosmos DB |Как tooread из базы данных Azure Cosmos. |
| Пример модуля записи Storm Azure Cosmos DB |Как toowrite tooAzure Cosmos DB. |
| Пример модуля чтения концентратора событий Storm |Как tooread из концентраторов событий Azure. |
| Пример модуля записи концентратора событий Storm |Как toowrite tooAzure концентраторов событий. |
| Пример модуля чтения Storm HBase |Как кластеры tooread из HBase на HDInsight. |
| Пример модуля записи Storm HBase |Как кластеры tooHBase toowrite на HDInsight. |
| Пример Storm Hybrid |Как toouse компонента Java. |
| Пример Storm |Базовая топология подсчета слов. |

> [!WARNING]
> Не все шаблоны будут работать с HDInsight под управлением Linux. Пакеты NuGet, используемые hello шаблоны могут оказаться несовместимыми с моно. Проверьте hello [моно совместимости](http://www.mono-project.com/docs/about-mono/compatibility/) документов и использовать hello [анализатор переносимости .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify потенциальных проблем.

В hello в данном пошаговом руководстве вы используете hello основные приложения Storm проекта типа toocreate топологии.

### <a name="hbase-templates-notes"></a>Заметки о шаблонах HBase

Hello HBase чтения и записи шаблоны использовать hello HBase REST API, не hello API-интерфейса Java HBase toocommunicate с HBase на HDInsight кластера.

### <a name="eventhub-templates-notes"></a>Заметки о шаблонах EventHub

> [!IMPORTANT]
> Hello EventHub на основе Java spout компонент, входящий в состав hello чтения EventHub шаблона не может работать с Storm в HDInsight версии 3.5 или более поздней версии. Обновленная версия этого компонента доступна в [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Пример топологии, которая использует этот компонент и работает со Storm в HDInsight 3.5, см. в [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Создание топологии на C#

1. Откройте Visual Studio, выберите **Файл** > **Создать**, а затем — **Проект**.

2. Из hello **новый проект** окна, разверните **установленные** > **шаблоны**и выберите **Озера данных Azure**. Выберите из списка шаблонов hello **Storm приложения**. Hello нижней части экрана приветствия, введите **WordCount** как hello имя приложения hello.

    ![Снимок экрана: окно "Новый проект"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. После создания проекта hello должно быть hello следующие файлы:

   * **Program.cs**: этот файл определяет hello топологии для вашего проекта. Обратите внимание, что по умолчанию создается топология, состоящая из одного объекта spout и одного объекта bolt.

   * **Spout.cs**— пример воронки, выдающей случайные числа.

   * **Bolt.cs**: пример молнии, отслеживает количество чисел, генерируемой hello spout.

     При создании проекта hello NuGet загрузки последних hello [SCP.NET пакета](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Реализуйте spout hello

1. Откройте файл **Spout.cs**. Spouts, используемые tooread данных в топологии из внешнего источника. Hello основных компонентов для spout входят:

   * **NextTuple**: вызывается Storm при hello spout допускается tooemit новые кортежи.

   * **ACK** (только для транзакций топология): обрабатывает подтверждений, инициированное другим компонентам в топологии hello для кортежей, присланные hello spout. Подтверждение кортеж позволяет spout hello знать, что он был успешно обработан, нижестоящим компонентам.

   * **Сбой** (только для транзакций топология): обрабатывает кортежи, сбой обработки других компонентов в топологии hello. Реализация метода Fail позволяет toore-порождение hello кортежа, чтобы можно было обработать еще раз.

2. Замените содержимое hello hello **Spout** класса после текста hello. Это spout случайным образом выдает предложения в топологию hello.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Реализовать винты hello

1. Удалить существующую hello **Bolt.cs** файл из проекта hello.

2. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **добавить** > **новый элемент**. Выберите из списка hello **молнии Storm**и введите **Splitter.cs** имени hello. Повторите этот процесс toocreate, с именем второго молнии **Counter.cs**.

   * **Splitter.cs** — реализует элемент bolt, который делит предложения на отдельные слова и выдает новый поток слов.

   * **Counter.cs**: реализует молнии, который подсчитывает каждого слова и создает новый поток ключевых слов и hello счетчик для каждого слова.

     > [!NOTE]
     > Эти элементы на чтение и запись toostreams, но можно также использовать toocommunicate молнии с источников, таких как базы данных или службы.

3. Откройте файл **Splitter.cs**. Он содержит только один метод по умолчанию — **Execute**. Hello метод Execute вызывается при молнии hello получает кортеж для обработки. Здесь можно считывать и обрабатывать входящие кортежи и создавать исходящие кортежи.

4. Замените содержимое hello hello **разделителей** класса hello, следующий код:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Откройте **Counter.cs**и замените содержимое класса hello hello следующее:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Определение топологии hello

Spouts и винты выстроены в виде графа, который определяет направление потока данных hello между компонентами. Для реализации этой топологии hello graph выглядит следующим образом:

![Схема компонентов](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Предложения создаются из hello spout и являются распределенные tooinstances молнии разделителей hello. Hello разделителей молнии разбивает hello предложений на слова, являющиеся распределенных toohello счетчика молнии.

Так как статистика хранится локально в экземпляр счетчика hello, мы хотим убедиться, что конкретные слова потока toohello toomake же экземпляром счетчика молнии. Каждое конкретное слово отслеживается только одним экземпляром. Поскольку молнии разделителей hello не поддерживает состояние, действительно неважно, какой экземпляр разделителей hello получает какие предложения.

Откройте файл **Program.cs**. Hello важный метод — **GetTopologyBuilder**, которой используется toodefine hello топологии, отправляется tooStorm. Замените содержимое hello **GetTopologyBuilder** с hello, следующий код tooimplement hello топологии, описанные выше:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Отправить hello топологии

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.

   > [!NOTE]
   > При появлении запроса введите учетные данные hello подписки Azure. При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.

2. Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**. Можно отслеживать при отправке hello успешной с помощью hello **вывода** окна.

3. При успешной отправки топологии hello hello **Storm топологии** для hello кластера должны отображаться. Выберите hello **WordCount** топологию с hello список tooview сведения о hello под управлением топологии.

   > [!NOTE]
   > **Топологии Storm** можно также просмотреть в **обозревателе сервера**. Разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши элемент "Storm" в кластере HDInsight и выберите пункт **Просмотреть топологии Storm**.

    tooview сведения о компонентах hello в топологии hello, дважды щелкните компонент hello в диаграмме hello.

4. Из hello **топологии Сводка** щелкните **Kill** toostop hello топологии.

   > [!NOTE]
   > Топологии storm продолжения toorun они будут отключены или удалены hello кластера.

## <a name="transactional-topology"></a>Транзакционная топология

Топология предыдущей Hello является нетранзакционной. в топологии hello компоненты Hello не реализуют функциональность tooreplaying сообщений. Пример топологии транзакций, создайте проект и выберите **Storm пример** hello тип проекта.

Реализуйте hello транзакций топологии, после воспроизведения toosupport данных:

* **Кэширование метаданных**: hello spout необходимо хранить метаданные о данных hello, получится, hello данных можно извлечь и повторно создаваться в случае возникновения сбоя. Из-за малого данных hello, генерируемой образец hello hello необработанные данные для каждого кортежа хранятся в словаре для воспроизведения.

* **ACK**: каждый молнии в топологии hello можно вызвать `this.ctx.Ack(tuple)` tooacknowledge, что кортеж обработана успешно. Здравствуйте, если все элементы имеют запись hello кортежа, `Ack` будет вызван метод hello spout. Hello `Ack` метод позволяет hello spout tooremove данные, которые были сохранены для воспроизведения.

* **Сбой**: каждый молнии можно вызвать `this.ctx.Fail(tuple)` tooindicate сбой обработки для кортеж. Сбой Hello распространяет toohello `Fail` метод spout hello, где могут быть воспроизведены hello кортежа с помощью кэшированные метаданные.

* **Sequence ID**(Идентификатор последовательности) — при отправке кортежа может быть указан уникальный идентификатор последовательности. Это значение определяет hello кортежа для обработки воспроизведения (Ack и сбоя). Например, hello spout в hello **Storm образец** проект использует следующие hello при отправке данных:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Этот код создает кортеж, содержащий поток по умолчанию toohello предложения и значением идентификатора последовательности hello, содержащихся в **lastSeqId**. В этом примере **lastSeqId** увеличивается после каждой отправки кортежа.

Как показано в hello **Storm пример** проекта, является ли компонент транзакций можно задать во время выполнения, в зависимости от конфигурации.

## <a name="hybrid-topology-with-c-and-java"></a>Гибридная топология с помощью C# и Java

Также можно использовать средства Озера данных для Visual Studio toocreate гибридной топологии, где некоторые компоненты являются C#, а другие — Java.

Чтобы получить пример гибридной топологии, создайте проект и выберите **Пример гибридного решения Storm**. Этот образец демонстрирует следующие основные понятия hello:

* **Компонент spout на Java** и **элемент bolt на C#** — определены в **HybridTopology_javaSpout_csharpBolt**.

    * Транзакционная версия определена в **HybridTopologyTx_javaSpout_csharpBolt**.

* **Компонент spout на C#** и **элемент bolt на Java** — определены в **HybridTopology_csharpSpout_javaBolt**.

    * Транзакционная версия определена в **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Эта версия также демонстрирует, как toouse Clojure код из текстового файла, как компонент Java.


Топология hello tooswitch, используемый при отправке hello проекта просто переместить hello `[Active(true)]` инструкции toohello топологии требуется toouse, перед его отправкой toohello кластера.

> [!NOTE]
> Все файлы hello Java, которые необходимы предоставляются как часть этого проекта в hello **JavaDependency** папки.

При создании и отправке гибридной топологии, рассмотрим следующие hello.

* Необходимо использовать **JavaComponentConstructor** toocreate экземпляр hello класс Java для spout или молнии.

* Следует использовать **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON объекты tooserialize данных в таблицу или из компонентов Java из Java.

* При отправке hello топологии toohello сервера, необходимо использовать hello **дополнительных конфигураций** hello параметр toospecify **пути к файлам Java**. Указанный путь Hello следует hello каталог, содержащий файлы JAR hello, содержащие классы Java.

### <a name="azure-event-hubs"></a>Концентраторы событий Azure

Версии SCP.NET 0.9.4.203 появился новый класс и метод специально для работы с spout hello концентратора событий (Java spout, который считывает данные из концентраторов событий). При создании топологии, которая использует spout концентратора событий, используйте hello следующие методы:

* **EventHubSpoutConfig** класса: создает объект, содержащий конфигурацию hello hello spout компонента.

* **TopologyBuilder.SetEventHubSpout** метод: Добавляет hello концентратора событий spout компонент toohello топологии.

> [!NOTE]
> Необходимо использовать hello **CustomizedInteropJSONSerializer** tooserialize данных, полученных при hello spout.

## <a id="configurationmanager"></a>Использование ConfigurationManager

Не используйте **ConfigurationManager** значения конфигурации tooretrieve винта и spout компонентов. Это вызовет исключение пустого указателя. Вместо этого hello конфигурацию для проекта передается в топологию Storm hello как пара ключ-значение в контексте топологии hello. Каждый компонент, зависят от значений конфигурации необходимо извлечь их из контекста hello во время инициализации.

Hello следующий код демонстрирует, как tooretrieve следующих значений:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

При использовании `Get` tooreturn метод экземпляра компонента, необходимо убедиться, передачей обоих hello `Context` и `Dictionary<string, Object>` toohello конструктор параметров. Hello следующий пример представляет собой простую `Get` метод, который неправильно передает эти значения:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Как tooupdate SCP.NET

Последние версии SCP.NET поддерживают обновление пакета через NuGet. Если доступно новое обновление, вы получите уведомление об обновлении. Проверка toomanually обновления, выполните следующие действия.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **управление пакетами NuGet**.

2. Диспетчер пакетов hello, выберите **обновления**. Если обновление доступно, оно будет отображено. Нажмите кнопку **обновление** для hello пакета tooinstall его.

> [!IMPORTANT]
> Если проект был создан в более ранней версии, не использующим NuGet SCP.NET, необходимо выполнить следующие шаги tooupdate tooa более новая версия hello:
>
> 1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **управление пакетами NuGet**.
> 2. С помощью hello **поиска** поле, поиск и затем добавить **Microsoft.SCP.Net.SDK** toohello проекта.

## <a name="troubleshoot-common-issues-with-topologies"></a>Устранение распространенных неполадок с топологиями

### <a name="null-pointer-exceptions"></a>Исключение пустого указателя

При использовании топологии на C# с кластером HDInsight под управлением Linux винта и компоненты, которые используют spout **ConfigurationManager** tooread параметры конфигурации во время выполнения может возвращать исключение указателя null.

Hello конфигурацию для проекта передается в топологию Storm hello как пара ключ-значение в контексте топологии hello. Его можно извлечь из объекта hello словарь, который передается tooyour компонентов после их инициализации.

Дополнительные сведения см. в разделе hello [ConfigurationManager](#configurationmanager) раздел этого документа.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

При использовании топологии на C# с кластером HDInsight под управлением Linux, может возникнуть следующая ошибка hello:

    System.TypeLoadException: Failure has occurred while loading a type.

Эта ошибка возникает при использовании двоичного файла, несовместим с версией .NET, которая поддерживает моно hello.

Для кластеров HDInsight под управлением Linux в проекте должны использоваться двоичные файлы, скомпилированные для .NET 4.5.

### <a name="test-a-topology-locally"></a>Локальная проверка топологии

Несмотря на то, что это просто toodeploy кластера tooa топологии, в некоторых случаях может потребоваться tootest топологии локально. Используйте следующие шаги toorun hello и протестировать пример топологии hello в этом учебнике локально в среде разработки.

> [!WARNING]
> Локальное тестирование работает только для базовых топологий на C#. Нельзя использовать локальное тестирование для гибридных топологий или топологий, использующих несколько потоков.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **свойства**. В свойствах проекта hello, измените hello **тип вывода** слишком**консольное приложение**.

    ![Снимок экрана: свойства проекта с выделенным свойством "Тип выходных данных"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Запомнить toochange hello **тип вывода** резервное слишком**библиотеки классов** перед развертыванием кластера tooa топологии hello.

2. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **добавить** > **новый элемент**. Выберите **класса**и введите **LocalTest.cs** имени класса hello. Теперь нажмите кнопку **Добавить**.

3. Откройте **LocalTest.cs**и добавьте следующее hello **с помощью** в начало hello инструкцию:

    ```csharp
    using Microsoft.SCP;
    ```

4. Используйте hello следующий код в том, как содержимое hello hello **LocalTest** класса:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Занять некоторое время tooread через hello комментарии к коду. Этот код использует **LocalContext** toorun hello компонентов в среде разработки hello и он будет повторяться hello потока данных между файлами tootext компонентов на локальном диске hello.

1. Откройте **Program.cs**и добавьте следующие toohello hello **Main** метод:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Сохранить изменения hello и нажмите кнопку **F5** или выберите **отладки** > **начать отладку** toostart hello проекта. Окно консоли должен отображаться, а также состояние журнала в ходе тестов hello. При **завершения тестов** появится, нажмите любое окно hello tooclose ключа.

3. Используйте **Проводник** toolocate hello каталог, содержащий проект. например **C:\Users\<имя_пользователя>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**. В этом каталоге откройте **Bin**, а затем щелкните **Отладка**. Вы увидите hello текстовые файлы, которые были созданы при выполнении тестов hello: sentences.txt, counter.txt и splitter.txt. Откройте каждый текстовый файл и просматривать данные hello.

   > [!NOTE]
   > Строковые данные сохраняются в этих файлах как массив значений типа decimal. Например, \[[97,103,111]] в hello **splitter.txt** файла — слово hello *и*.

> [!NOTE]
> Быть убедиться, что hello tooset **тип проекта** резервное слишком**библиотеки классов** перед развертыванием tooa Storm в кластере HDInsight.

### <a name="log-information"></a>Информация о журнале

С помощью `Context.Logger`можно легко записывать информацию из компонентов топологии в журнал. Например следующие hello создается запись журнала сведений:

```csharp
Context.Logger.Info("Component started");
```

Записанные данные можно просмотреть hello **входа службы Hadoop**, расположенное в **обозревателя серверов**. Разверните запись hello для вашего ураган в кластере HDInsight, а затем разверните **входа службы Hadoop**. Наконец выберите файл tooview hello журнала.

> [!NOTE]
> Hello журналы хранятся в учетной записи хранилища Azure, используемой кластером hello. журналы hello tooview в Visual Studio, необходимо войти в toohello подписки Azure, которой принадлежит учетная запись хранения hello.

### <a name="view-error-information"></a>Просмотр информации об ошибке

tooview ошибки, произошедшие в топологии выполняющегося hello используйте следующие шаги:

1. Из **обозревателя серверов**, щелкните правой кнопкой мыши hello ураган в кластере HDInsight и выберите **Storm представление топологии**.

2. Для hello **Spout** и **болтов**, hello **последней ошибки** столбец содержит сведения о последней ошибке hello.

3. Выберите hello **Spout идентификатор** или **молнии идентификатор** hello компонента, который содержит ошибку в списке. На странице приветствия, ошибка отображается, Дополнительные сведения о указана в hello **ошибки** раздел hello нижней части страницы приветствия.

4. tooobtain Дополнительные сведения, **порт** из hello **исполнителей** раздел страницы приветствия, toosee hello Storm работника в журнале hello последние несколько минут.

### <a name="errors-submitting-topologies"></a>Ошибки при отправке топологии

Если возникают ошибки при отправке tooHDInsight топологии, можно найти журналы для hello серверные компоненты, обрабатывающие топологии отправки в кластере HDInsight. Эти журналы, tooretrieve hello используйте следующую команду из командной строки:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Замените __sshuser__ с hello SSH учетной записи пользователя для кластера hello. Замените __clustername__ с именем hello hello кластера HDInsight. Дополнительные сведения об использовании `scp` и `ssh` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Отправка может завершиться ошибкой по нескольким причинам:

* JDK не установлен или не находится в пути hello.
* Необходимые зависимости Java не включаются в отправки hello.
* Несовместимые зависимости.
* Повторяющиеся имена топологий.

Если hello `hdinsight-scpwebapi.out` журнал содержит `FileNotFoundException`, это может быть вызвано hello следующие условия:

* Hello JDK не hello пути в среде разработки hello. Убедитесь, что hello JDK установлен в среде разработки hello и что `%JAVA_HOME%/bin` находится в папке hello.
* Отсутствует зависимость Java. Убедитесь, что все файлы, необходимые .jar включаются как часть отправки hello.

## <a name="next-steps"></a>Дальнейшие действия

Пример обработки данных из концентраторов событий см. в статье [Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Пример топологии C#, которая разбивает поток данных на несколько потоков, см. на странице с [примером C# Storm](https://github.com/Blackmist/csharp-storm-example).

см. Дополнительные сведения о создании C# топологий, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Дополнительные способы toowork с HDInsight и дополнительные Storm об образцах, HDInsight см hello следующие документы:

**Microsoft SCP.NET**

* [Руководство по программированию для SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm в HDInsight**

* [Развертывание и мониторинг топологии с помощью Apache Storm в HDInsight.](hdinsight-storm-deploy-monitor-topology.md)
* [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop в HDInsight**

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase в HDInsight**

* [Начало работы с HBase в HDInsight](hdinsight-hbase-tutorial-get-started.md)
