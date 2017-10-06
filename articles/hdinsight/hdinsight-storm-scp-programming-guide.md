---
title: "руководство по программированию aaaSCP.NET | Документы Microsoft"
description: "Узнайте, как toouse SCP.NET toocreate. На основе NET Storm топологии для использования с Storm на HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>Руководство по программированию для SCP
Точка подключения службы — это платформа toobuild реального времени надежной, согласованной и высокой производительности приложение обработки данных. Строится на основе [Apache Storm](http://storm.incubator.apache.org/) --потоковой обработки системы, разработанная hello OSS сообщества. Создателем Storm является Натан Марц (Nathan Marz), программа имеет открытый код и распространяется компанией Twitter. Он использует [Apache ZooKeeper](http://zookeeper.apache.org/), другой Apache проекта tooenable высоконадежными распределенных координации и управления состоянием. 

Не только проект hello SCP перенесена ураган в Windows, но также добавить проект hello расширения и настройки для экосистемы Windows hello. Hello расширения включают работу разработчиков .NET и библиотеках, настройки hello включает развертывание на основе Windows. 

расширение Hello и настройки выполняется таким образом, что проекты OSS toofork hello не требуется, и нам удалось использовать производном экосистемы построена на базе Storm.

## <a name="processing-model"></a>Модель обработки данных
данные Hello в SCP моделируется как непрерывные потоки кортежей. Обычно кортежей hello поступать в некоторых очередь, сначала, а затем выборка и преобразование бизнес-логики, размещенные внутри топологии Storm, наконец hello выходных данных может быть выведен как система tooanother SCP кортежей или быть зафиксирована toostores распределенной файловой системы, например или базы данных, например SQL Server.

![Схема очереди, передав tooprocessing данные, какие каналы в хранилище данных](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

В Storm вычислительные графы определяются топологией приложения. Каждый узел в топологии содержит логическую схему обработки информации, а по связям между узлами можно определить движение потока данных. Hello узлы tooinject входных данных в топологии hello, называются Spouts, которые могут быть данных используется toosequence hello. Hello входных данных может находиться в файлы журналов транзакций базы данных, счетчик производительности системы и т.д. hello узлов с обоих потоках ввода-вывода данных, называются элементы, которые hello фильтрации фактических данных и выбора и статистической обработки.

SCP поддерживает максимальное качество работы при типе обработки данных "минимум однажды" и "только однажды". В распределенном приложении для обработки потоковой передачи могут возникать различные ошибки во время обработки данных, например сбой сети, аппаратный сбой, ошибка в коде пользователя и т. п. В Однократная обработка обеспечивает все данные будут обработаны по крайней мере один раз путем воспроизведения автоматически hello и тех же данных в случае ошибки. Модель обработки "только однажды" проста и надежна и отлично подходит для многих приложений. Однако если hello приложение требует точного подсчета, например, в Однократная обработка недостаточно поскольку hello и те же данные может потенциально воспроизводиться в топологии приложения hello. В этом случае, точно-после обработки предназначен toomake убедиться, что результат hello правильность даже в том случае, если данные hello могут воспроизведения и обрабатываться несколько раз.

Точка подключения службы позволяет приложениям, процесс .NET разработчики toodevelop реального времени данных при hello использование виртуальной машины Java (JVM) на основе Storm под титульных hello. Hello .NET и виртуальной машины Java связь через локального сокета TCP. По сути каждого Spout/молнии является парой процесса .net/Java где логики hello пользователя выполняется в процессе .net, что подключаемый модуль.

toobuild приложения на основе SCP обработки данных, требуются несколько шагов:

* Разрабатывать и реализовывать hello Spouts toopull в данные из очереди.
* Разработать и реализовать винты tooprocess hello входных данных и сохранить tooexternal хранилищ данных, таких как базы данных.
* Разрабатывайте топологию hello, отправки и запуска топологии hello. Hello Топология определяет вершин и hello данные потоков между hello вершин. Точка подключения службы будет принимать спецификацию топологии hello и развернуть ее на кластер Storm, где выполняется Каждая вершина на одном узле логических. отработка отказа Hello и масштабирование будет возложить планировщиком hello Storm.

В этом документе будет использовать некоторые простые примеры toowalk как toobuild приложения обработки данных с точки подключения службы.

## <a name="scp-plugin-interface"></a>Интерфейс подключаемого модуля SCP
Подключаемые модули точка подключения службы (или приложения), автономный EXE-файлов можно работают в среде Visual Studio на этапе разработки hello, которые следует подключать hello Storm конвейера после развертывания в рабочей среде. Hello SCP подключаемого модуля записи просто Здравствуйте, то же, что записи любые другие стандартные приложения консоли Windows. Платформа SCP.NET объявляет интерфейс для spout/молнии и эти интерфейсы следует реализовывать hello пользовательского подключаемого модуля кода. главной задачей Hello этой конструкции является этот пользователь hello позволяет сосредоточиться на своих собственных бизнес-логики и оставляя toobe другие вещи, обрабатываемых SCP.NET платформы.

Hello пользовательского подключаемого модуля кода должен реализовывать один из интерфейсов hello следующие действия, зависит ли топологии hello транзакционной или нетранзакционной, и является ли компонент hello spout или молнии.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin — hello общий интерфейс для всех видов подключаемых модулей. В данном случае мы работаем с имитатором интерфейса.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout является интерфейсом hello для нетранзакционных spout.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Когда `NextTuple()` вызывается hello C\# пользовательский код можно создавать один или несколько раз. Если нет ничего tooemit, этот метод должен возвращать без передачи ничего. Нужно отметить, что команды `NextTuple()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#. При наличии не tooemit кортежей, — спящий режим NextTuple вежливость toohave для за короткий промежуток времени (например, 10 миллисекунд), поскольку не toowaste чрезмерно загружающих ЦП.

Команды `Ack()` и `Fail()` вызываются только в случае активации механизма подтверждения в файле спецификации. Hello `seqId` представляет кортеж используется tooidentify hello, или не удалось выполнить запись. Поэтому если ack включен нетранзакционный топологии, следует использовать после выдачи функции hello в Spout:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Здравствуйте, если ack не поддерживается в топологии нетранзакционной, `Ack()` и `Fail()` можно оставить пустым функции.

Hello `parms` входные параметры в эти функции являются просто пустой словарь, они зарезервированы для будущего использования.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt является интерфейсом hello для нетранзакционных молнии.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Если доступен новый кортежа, hello `Execute()` функция будет вызываться tooprocess его.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout является интерфейсом hello для spout транзакций.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Так же как и в случае с нетранзакционными воронками, команды `NextTx()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#. При наличии tooemit нет данных, он используется вежливость toohave `NextTx` спящий режим на короткий период времени (10 миллисекунд), поскольку не toowaste чрезмерно загружающих ЦП.

`NextTx()`вызывается toostart новую транзакцию, hello выходной параметр `seqId` транзакция используется tooidentify hello, используемый в `Ack()` и `Fail()`. В `NextTx()`, пользователя можно создавать стороне tooJava данных. Hello данные будут храниться в ZooKeeper toosupport воспроизведения. Поскольку hello емкости ZooKeeper не ограничены, пользователя только должны предоставлять метаданные, не массового данных транзакций spout.

Storm автоматически повторит транзакцию, если она завершилась с ошибкой, поэтому в нормальных условиях `Fail()` вызывать не следует. Но если точка подключения службы можно проверить метаданные hello, генерируемой транзакций spout, оно может вызвать `Fail()` при hello метаданные являются недопустимыми.

Hello `parms` входные параметры в эти функции являются просто пустой словарь, они зарезервированы для будущего использования.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt является интерфейсом hello для транзакций молнии.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`вызывается при наличии нового кортежа, поступающих в hello молнии. `FinishBatch()` вызывается после завершения этой транзакции. Hello `parms` входной параметр зарезервирован для будущего использования.

Для транзакционной топологии существует важная концепция — `StormTxAttempt`. Она содержит два поля: `TxId` и `AttemptId`. `TxId`является используется tooidentify определенной транзакции, и для данной транзакции может существовать несколько попыток при сбое транзакции hello воспроизведения. SCP.NET новые будет другой ISCPBatchBolt объекта tooprocess каждого `StormTxAttempt`точно так же, как чего Storm стороне Java. смысл этой конструкции Hello — toosupport обработки параллельных транзакций. Пользователю необходимо учитывать его, если завершения попытки транзакции, соответствующего объекта ISCPBatchBolt hello будут уничтожены и сборщиком мусора.

## <a name="object-model"></a>Объектная модель
SCP.NET также предоставляет простой набор ключевых объектов для разработчиков tooprogram с. В их число входят: **Context**, **StateStore** и **SCPRuntime**. Они обсуждаются в hello остальной части этого раздела.

### <a name="context"></a>Context
Контекст предоставляет работающее приложение toohello среды. Каждому экземпляру дополнительного модуля ISCP (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) соответствует экземпляр объекта Context. Hello функциональные возможности, предоставляемые контекст можно разделить на две части: статическую часть hello (1), которое доступно в hello всей C\# обработки динамической части hello (2), который доступен только для конкретного экземпляра контекстного hello.

### <a name="static-part"></a>Статическая часть
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` отвечает за создание записей в журнале.

`pluginType`— используется тип подключаемого модуля hello tooindicate hello C\# процесса. Если hello C\# процесс выполняется в локальном режиме (без Java), тип подключаемого модуля hello `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`предоставляется tooget параметры конфигурации со стороны Java. Hello параметры передаются со стороны Java при C\# инициализации подключаемого модуля. Hello `Config` параметры делятся на две части: `stormConf` и `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`— параметров, определенных Storm и `pluginConf` — hello параметров, определенных точка подключения службы. Например:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`предоставляется tooget hello топологии контекста, это может пригодиться, для компонентов с несколькими параллелизма. Пример:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Динамическая часть
Здравствуйте, следующие интерфейсы являются нужные tooa экземпляром определенного контекста. экземпляр контекста Hello создается платформой SCP.NET и передается toohello пользовательского кода:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Для поддержки ack нетранзакционных spout предоставляется hello следующий метод:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Для нетранзакционных молнии поддержки ack, должны явным образом `Ack()` или `Fail()` hello кортежа, оно получено. А при выдаче нового кортежа, его необходимо задать привязки hello hello новый кортежа. предоставляются следующие методы Hello.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` предоставляет службы метаданных, создание монотонных последовательностей и координацию без ожидания. Распределенные многозадачные абстракции высокого уровня могут создаваться на базе `StateStore`, включая создание распределенных блокировок, распределенных очередей, барьеров и служб транзакций.

Точка подключения службы приложения могут использовать hello `State` объекта toopersist некоторые сведения в ZooKeeper, особенно для транзакционной топологии. . Таким образом, если транзакций spout аварийно завершает работу и перезапустите, он мог получить необходимую информацию hello из ZooKeeper и перезапустите hello конвейера.

Hello `StateStore` объекта в основном включает следующие методы:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Hello `State` объекта в основном включает следующие методы:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Для hello `Commit()` при метод simpleMode задано tootrue, он просто удалит соответствующие ZNode в ZooKeeper hello. В противном случае он будет удален текущий ZNode hello и Добавление нового узла в hello ЗАФИКСИРОВАНО\_пути.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime предоставляет следующие два метода hello.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`Представляет среду выполнения используется tooinitialize hello точка подключения службы. В этом методе hello C\# процесс будет подключаться стороне toohello Java и возвращает параметры конфигурации и топологии контекста.

`LaunchPlugin()`используется tookick off приветственное сообщение, обрабатывает цикла. В этом цикле hello C\# подключаемого модуля, получат сообщения форму стороны Java (включая кортежей и сигналов управления), а затем обрабатывать сообщения hello, может быть вызов метода интерфейса hello укажите с помощью пользовательского кода hello. Hello входного параметра для метода `LaunchPlugin()` является делегатом, который может возвращать объект, который реализует интерфейс ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Для ISCPBatchBolt, мы можем получить `StormTxAttempt` из `parms`и использовать его toojudge, будь то воспроизводимой попытки. Обычно это делается на молнии фиксации hello и демонстрируется hello `HelloWorldTx` примере.

Вообще говоря hello SCP подключаемые модули запускаются в двух режимах здесь:

1. Локальный режим теста: В этом режиме hello SCP подключаемых модулей (hello C\# пользовательского кода) выполняются в Visual Studio на этапе разработки hello. `LocalContext`может использоваться в этом режиме, который предоставляет метод tooserialize hello создается кортежей toolocal файлов и чтение их откат toomemory.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Обычный режим: В этом режиме подключаемых модулей SCP hello запущенных процессом java storm.
   
    Ниже дан пример запуска дополнительного модуля SCP:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Язык спецификации топологии
Спецификация топологии SCP представляет собой специализированный язык для описания и настройки топологий SCP. Он основан на Clojure DSL для Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) и расширен с помощью SCP.

Спецификации топологии, которые можно отправить непосредственно toostorm кластера для выполнения через hello ***runspec*** команды.

SCP.NET имеет добавить следующие функции toodefine hello транзакций топологии:

| **Новые функции** | **Параметры** | **Описание** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Определение топологии транзакций с именем hello топологии, &nbsp;spouts определения карты и карты определение винты hello |
| **scp-tx-spout** |exec-name<br />args<br />fields |Определение транзакционной "воронки". Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.<br /><br />Hello ***поля*** является hello выходные данные поля для spout |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |Определение транзакционного пакетного "сита". Он будет выполняться приложение hello с ***exec имя*** с помощью ***args.***<br /><br />Hello поля — hello вывод полей для молнии. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |Определение транзакционного подтверждающего "сита" Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.<br /><br />Hello ***поля*** — hello вывод полей для молнии |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Определение топологии нетранзакционной с именем hello топологии,&nbsp; spouts определения карты и карты определение винты hello |
| **scp-spout** |exec-name<br />args<br />fields<br />parameters |Определение нетранзакционной "воронки". Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.<br /><br />Hello ***поля*** является hello выходные данные поля для spout<br /><br />Hello ***параметры*** является необязательным, с помощью toospecify некоторые параметры, такие как «nontransactional.ack.enabled». |
| **scp-bolt** |exec-name<br />args<br />fields<br />parameters |Определение нетранзакционного "сита". Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.<br /><br />Hello ***поля*** — hello вывод полей для молнии<br /><br />Hello ***параметры*** является необязательным, с помощью toospecify некоторые параметры, такие как «nontransactional.ack.enabled». |

Для SCP.NET определены следующие ключевые слова:

| **Ключевые слова** | **Описание** |
| --- | --- |
| **:name** |Определите имя топологии hello |
| **:topology** |Определение топологии с помощью hello выше функции hello и сборку в коллекции. |
| **:p** |Определите hello указание параллелизма для каждого spout или молнии. |
| **:config** |Определите настройки параметра или обновление hello существующих |
| **:schema** |Определите hello схемы потока. |

И часто используемые параметры:

| **Параметр** | **Описание** |
| --- | --- |
| **"plugin.name"** |Имя файла EXE-файл подключаемого модуля hello C# |
| **"plugin.args"** |Аргументы параметров дополнительного модуля |
| **"output.schema"** |Схема вывода |
| **"nontransactional.ack.enabled"** |Если подтверждение обработки для нетранзакционной топологии активно. |

Команда runspec Hello будут развернуты вместе с hello bits, использование hello как:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hello ***ресурсов dir*** параметр является необязательным, вы должны toospecify его при необходимости tooplug C\# приложения и этот каталог будет содержать приложения hello, зависимости hello и конфигурации.

Hello ***classpath*** также не является обязательным. Это используется toospecify hello Java classpath, если файл характеристик hello содержит Java Spout или молнии.

## <a name="miscellaneous-features"></a>Прочие функции
### <a name="input-and-output-schema-declaration"></a>Объявление схемы ввода и вывода
Hello пользователя может выдавать кортежа в языке C\# обработки, hello платформа должна tooserialize hello кортежа в byte [], передача tooJava стороне и Storm передаст этой цели toohello кортежа. В то же время в нижестоящего компонента hello C\# процесс получения кортежа обратно стороне java и преобразовать исходные типы toohello платформой, все эти операции скрыты по hello платформы.

toosupport hello сериализации и десериализации, пользовательский код должен схемы hello toodeclare hello входов и выходов.

Схема потока ввода вывода Hello определен как словарь hello ключом hello StreamId и hello значение — hello типы столбцов hello. Hello компонент может иметь несколько потоков, которые объявлены.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


В контексте объекта у нас есть hello добавлены следующие API:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Пользовательский код необходимо убедиться, создавшего кортежей hello подчиняются hello схемой, определенной для этого потока, либо hello система выдает исключение времени выполнения.

### <a name="multi-stream-support"></a>Поддержка многопоточности
Точка подключения службы поддерживает пользователя кода tooemit или получать из нескольких различных потоков в hello же время. Поддержка Hello отражает hello объекта контекста как hello Emit метод принимает параметр ID дополнительный поток.

Были добавлены два метода в hello объекта SCP.NET контекста. Они являются используется tooemit кортеж или кортежи toospecify StreamId. Hello StreamId — это строка, а также он должен toobe согласованность обоих C\# и hello Spec определения топологии.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

Hello выпускающей tooa несуществующего потока вызовут исключения среды выполнения.

### <a name="fields-grouping"></a>Группирование полей
Hello сборки в группирование полей Strom работает неправильно в SCP.NET. На hello стороны Java прокси-сервера все типы данных полей hello, фактически byte [] и группирование полей hello использует hello byte [] объекта хэша кода tooperform hello группирования. хэш-код byte [] Hello объекта — адрес hello объекта в памяти. Таким образом, группирование hello неправильный для двух байтов [] объектов этой общей папке hello же содержимого, но не hello того же адреса.

SCP.NET добавляет метод настроенные группирования и будет использовать содержимое hello hello byte [] toodo hello группирования. В **SPEC** файл, синтаксис hello содержит:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


В данном случае

1. "scp-field-group" означает "адаптированный метод группирования полей с помощью SCP".
2. ":tx" или "non-tx" означает транзакционную или нетранзакционную топологию. Мы должны эти сведения, поскольку hello начальным индексом и топологии не tx отличается в tx.
3. [0,1] означает набор хэш-функций идентификаторов полей (начальное значение = "0").

### <a name="hybrid-topology"></a>Гибридная топология
машинный код Hello Storm написан на языке Java. И SCP.Net усовершенствованы его tooenable нашей правил toowrite C\# кода toohandle их бизнес-логике. Но мы также поддерживаем гибридные топологии, в которых воронки и сита возможны не только на C\#, но и на Java.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Задание "воронок" и "сит" на Java в файле спецификаций.
В спецификации файла «scp spout» и «scp молнии» также можно использовать toospecify Spouts Java и винты, ниже приведен пример:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Здесь `microsoft.scp.example.HybridTopology.Generator` — имя hello hello Java Spout класса.

### <a name="specify-java-classpath-in-runspec-command"></a>Указание classpath Java в команде runSpec
Следует toosubmit топологии, содержащий Java Spouts или винты требуется hello компиляции toofirst Java Spouts или винты и получить hello Jar-файла. Необходимо указать hello java classpath, содержащий hello Jar-файла при отправке топологии. Пример:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Здесь **примеры\\HybridTopology\\java\\целевой\\**  hello папку, содержащую файл Jar Spout/молнии Java hello.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Сериализация или десериализация между Java и C#
Компонент SCP включает в себя часть C\# и часть Java. В порядке toointeract с собственного Java Spouts/винты, сериализации и десериализации должно быть выполнено между границей Java и C\# стороны, как показано в следующих graph hello.

![Схема отправки tooSCP компонента отправки компонент tooJava компонента java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Сериализация на стороне Java и десериализация на стороне C\#**
   
   Для начала нужно обеспечить стандартное применение сериализации на стороне Java и десериализации на стороне C\#. метод сериализации Hello в сторону Java можно указать в файле характеристик:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Здравствуйте, метод десериализации в языке C\# стороны должно быть указано в C\# пользовательского кода:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Данная реализация по умолчанию должен обрабатывать большинстве случаев, если тип данных hello не является слишком сложным. В некоторых случаях либо поскольку hello пользовательского типа данных является слишком сложным или hello производительность реализацию по умолчанию не соответствует hello требований пользователя, пользователь может подключаемый модуль свою собственную реализацию.
   
   интерфейс сериализации Hello в java стороны определяется как:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Hello десериализации интерфейса в C\# стороне определяется как:
   
   Общедоступный интерфейс ICustomizedInteropCSharpDeserializer.
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Сериализация на стороне C\# и десериализация на стороне Java**
   
   Здравствуйте, метод сериализации в C\# стороны должно быть указано в C\# пользовательского кода:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   метод десериализации стороне Java Hello должно быть указано в СПЕЦИФИКАЦИИ файла:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Вот десериализатор hello имя «microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer» и «microsoft.scp.example.HybridTopology.Person» — для десериализации класса hello hello целевых данных.
   
   Пользователь может также подключить свою собственную реализацию сериализатора C\# и десериализатора Java. Это интерфейс hello для C\# сериализатор:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Это интерфейс hello для десериализатор Java:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Хост-режим SCP
В этом режиме пользователь можно скомпилировать их tooDLL коды и использовать SCPHost.exe предоставляемые SCP toosubmit топологии. Спецификация файла Hello выглядит следующим образом:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Здесь в качестве `plugin.name` указан `SCPHost.exe` из пакета SDK для SCP. SCPHost.exe принимает только три параметра:

1. Hello сначала он hello DLL имя, являющееся `"HelloWorld.dll"` в этом примере.
2. Hello второе — это имя класса hello, являющееся `"Scp.App.HelloWorld.Generator"` в этом примере.
3. Hello третий он hello имени общего статического метода, который может быть вызванным tooget экземпляр ISCPPlugin.

В хост-режиме код пользователя компилируется в DLL-файл и вызывается платформой SCP. Поэтому SCP платформы можно получить полный контроль над логику обработки всей hello. Поэтому рекомендуется наших клиентов toosubmit топологии в режиме SCP узла, так как его можно упростить процесс разработки hello и расскажи нам большую гибкость и лучше обратной совместимости для более поздней версии также.

## <a name="scp-programming-examples"></a>Примеры программирования для SCP
### <a name="helloworld"></a>HelloWorld
**HelloWorld** является tooshow очень простой пример, чтобы получить представление о SCP.Net. Она использует нетранзакционную топологию, в которой воронка называется **generator**, а два сита — **splitter** и **counter**. Hello spout **генератор** будет случайным образом создать некоторые предложения и передачи этих предложений слишком**разделителей**. Hello молнии **разделителей** будет разделить toowords предложений hello и создавать эти слова слишком**счетчика** молнии. Hello молнии «счетчик» используется ряд словарь hello toorecord вхождения каждого слова.

Для этого примера существует два файла спецификации — **HelloWorld.spec** и **HelloWorld\_EnableAck.spec**. В hello C\# кода, его можно узнать включении ack, обратившись hello pluginConf со стороны Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

При включении ack словарь в hello spout является используется toocache hello кортежей, которые не были запись. При вызове Fail() hello неудачных кортеж будет воспроизведен в:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Hello **HelloWorldTx** примере показано, как tooimplement транзакций топологии. В ней воронка называется **generator**, пакетные сита — **partial-count**, а подтверждающее сито — **count-sum**. В примере содержатся три предварительно созданных текстовых файла: **DataSource0.txt**, **DataSource1.txt** и **DataSource2.txt**.

В каждой транзакции hello spout **генератор** будет случайным образом выбрать два файла из ранее созданной три файла hello и передачи hello два файла имена toohello **частичного число** молнии. Hello молнии **частичного число** сначала нужно получить имя файла hello из полученных hello кортежа, а затем Привет открыть файл и число hello количество слов в этот файл и наконец порождение номеров toohello слово hello **счетчик сумма**молнии. Hello **сумма число** молнии будут использованы Помесячные hello общее число объектов.

tooachieve **ровно один раз** семантику, молнии фиксации hello **сумма число** требуется toojudge, будь то воспроизводимой транзакции. В этом примере транзакция имеет статическую переменную-член.

    public static long lastCommittedTxId = -1; 

Когда создается экземпляр ISCPBatchBolt, он получит hello `txAttempt` из входных параметров:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Когда `FinishBatch()` вызове hello `lastCommittedTxId` будет обновления, если это не воспроизводимой транзакции.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>Гибридная топология
Данная топология содержит воронку на Java и сито на C\#. Она использует hello реализация по умолчанию сериализации и десериализации SCP платформы. Пожалуйста, ref hello **HybridTopology.spec** в **примеры\\HybridTopology** папку hello характеристик сведений о файлах, и **SubmitTopology.bat** как toospecify Java classpath.

### <a name="scphostdemo"></a>SCPHostDemo
В этом примере hello аналогично HelloWorld в сущности. Hello единственным отличием является hello пользовательский код компилируется как библиотеки DLL и топологии hello передается с помощью SCPHost.exe. Более подробные объяснения, перенесите ref hello раздел «Режим узла SCP».

## <a name="next-steps"></a>Дальнейшие действия
Примеры топологий Storm, созданных с помощью точки подключения службы см. в следующем hello:

* [Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Создание нескольких потоков данных в топологии Storm на C#](hdinsight-storm-twitter-trending.md)
* [Использование Power Bi toovisualize данных из топологии Storm](hdinsight-storm-power-bi-topology.md)
* [Обработка данных с датчиков автомобиля из концентраторов событий с использованием Storm в HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Извлечения, преобразования и загрузки (ETL) из tooHBase концентраторов событий Azure](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Сопоставление событий с помощью Storm и HBase в HDInsight](hdinsight-storm-correlation-topology.md)

