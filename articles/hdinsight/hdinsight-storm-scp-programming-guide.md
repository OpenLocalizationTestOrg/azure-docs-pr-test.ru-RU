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
# <a name="scp-programming-guide"></a><span data-ttu-id="71ed0-103">Руководство по программированию для SCP</span><span class="sxs-lookup"><span data-stu-id="71ed0-103">SCP programming guide</span></span>
<span data-ttu-id="71ed0-104">Точка подключения службы — это платформа toobuild реального времени надежной, согласованной и высокой производительности приложение обработки данных.</span><span class="sxs-lookup"><span data-stu-id="71ed0-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="71ed0-105">Строится на основе [Apache Storm](http://storm.incubator.apache.org/) --потоковой обработки системы, разработанная hello OSS сообщества.</span><span class="sxs-lookup"><span data-stu-id="71ed0-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="71ed0-106">Создателем Storm является Натан Марц (Nathan Marz), программа имеет открытый код и распространяется компанией Twitter.</span><span class="sxs-lookup"><span data-stu-id="71ed0-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="71ed0-107">Он использует [Apache ZooKeeper](http://zookeeper.apache.org/), другой Apache проекта tooenable высоконадежными распределенных координации и управления состоянием.</span><span class="sxs-lookup"><span data-stu-id="71ed0-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="71ed0-108">Не только проект hello SCP перенесена ураган в Windows, но также добавить проект hello расширения и настройки для экосистемы Windows hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="71ed0-109">Hello расширения включают работу разработчиков .NET и библиотеках, настройки hello включает развертывание на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="71ed0-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="71ed0-110">расширение Hello и настройки выполняется таким образом, что проекты OSS toofork hello не требуется, и нам удалось использовать производном экосистемы построена на базе Storm.</span><span class="sxs-lookup"><span data-stu-id="71ed0-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="71ed0-111">Модель обработки данных</span><span class="sxs-lookup"><span data-stu-id="71ed0-111">Processing model</span></span>
<span data-ttu-id="71ed0-112">данные Hello в SCP моделируется как непрерывные потоки кортежей.</span><span class="sxs-lookup"><span data-stu-id="71ed0-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="71ed0-113">Обычно кортежей hello поступать в некоторых очередь, сначала, а затем выборка и преобразование бизнес-логики, размещенные внутри топологии Storm, наконец hello выходных данных может быть выведен как система tooanother SCP кортежей или быть зафиксирована toostores распределенной файловой системы, например или базы данных, например SQL Server.</span><span class="sxs-lookup"><span data-stu-id="71ed0-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Схема очереди, передав tooprocessing данные, какие каналы в хранилище данных](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="71ed0-115">В Storm вычислительные графы определяются топологией приложения.</span><span class="sxs-lookup"><span data-stu-id="71ed0-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="71ed0-116">Каждый узел в топологии содержит логическую схему обработки информации, а по связям между узлами можно определить движение потока данных.</span><span class="sxs-lookup"><span data-stu-id="71ed0-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="71ed0-117">Hello узлы tooinject входных данных в топологии hello, называются Spouts, которые могут быть данных используется toosequence hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="71ed0-118">Hello входных данных может находиться в файлы журналов транзакций базы данных, счетчик производительности системы и т.д. hello узлов с обоих потоках ввода-вывода данных, называются элементы, которые hello фильтрации фактических данных и выбора и статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="71ed0-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="71ed0-119">SCP поддерживает максимальное качество работы при типе обработки данных "минимум однажды" и "только однажды".</span><span class="sxs-lookup"><span data-stu-id="71ed0-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="71ed0-120">В распределенном приложении для обработки потоковой передачи могут возникать различные ошибки во время обработки данных, например сбой сети, аппаратный сбой, ошибка в коде пользователя и т. п. В Однократная обработка обеспечивает все данные будут обработаны по крайней мере один раз путем воспроизведения автоматически hello и тех же данных в случае ошибки.</span><span class="sxs-lookup"><span data-stu-id="71ed0-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="71ed0-121">Модель обработки "только однажды" проста и надежна и отлично подходит для многих приложений.</span><span class="sxs-lookup"><span data-stu-id="71ed0-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="71ed0-122">Однако если hello приложение требует точного подсчета, например, в Однократная обработка недостаточно поскольку hello и те же данные может потенциально воспроизводиться в топологии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="71ed0-123">В этом случае, точно-после обработки предназначен toomake убедиться, что результат hello правильность даже в том случае, если данные hello могут воспроизведения и обрабатываться несколько раз.</span><span class="sxs-lookup"><span data-stu-id="71ed0-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="71ed0-124">Точка подключения службы позволяет приложениям, процесс .NET разработчики toodevelop реального времени данных при hello использование виртуальной машины Java (JVM) на основе Storm под титульных hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="71ed0-125">Hello .NET и виртуальной машины Java связь через локального сокета TCP.</span><span class="sxs-lookup"><span data-stu-id="71ed0-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="71ed0-126">По сути каждого Spout/молнии является парой процесса .net/Java где логики hello пользователя выполняется в процессе .net, что подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="71ed0-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="71ed0-127">toobuild приложения на основе SCP обработки данных, требуются несколько шагов:</span><span class="sxs-lookup"><span data-stu-id="71ed0-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="71ed0-128">Разрабатывать и реализовывать hello Spouts toopull в данные из очереди.</span><span class="sxs-lookup"><span data-stu-id="71ed0-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="71ed0-129">Разработать и реализовать винты tooprocess hello входных данных и сохранить tooexternal хранилищ данных, таких как базы данных.</span><span class="sxs-lookup"><span data-stu-id="71ed0-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="71ed0-130">Разрабатывайте топологию hello, отправки и запуска топологии hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="71ed0-131">Hello Топология определяет вершин и hello данные потоков между hello вершин.</span><span class="sxs-lookup"><span data-stu-id="71ed0-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="71ed0-132">Точка подключения службы будет принимать спецификацию топологии hello и развернуть ее на кластер Storm, где выполняется Каждая вершина на одном узле логических.</span><span class="sxs-lookup"><span data-stu-id="71ed0-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="71ed0-133">отработка отказа Hello и масштабирование будет возложить планировщиком hello Storm.</span><span class="sxs-lookup"><span data-stu-id="71ed0-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="71ed0-134">В этом документе будет использовать некоторые простые примеры toowalk как toobuild приложения обработки данных с точки подключения службы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="71ed0-135">Интерфейс подключаемого модуля SCP</span><span class="sxs-lookup"><span data-stu-id="71ed0-135">SCP Plugin Interface</span></span>
<span data-ttu-id="71ed0-136">Подключаемые модули точка подключения службы (или приложения), автономный EXE-файлов можно работают в среде Visual Studio на этапе разработки hello, которые следует подключать hello Storm конвейера после развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="71ed0-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="71ed0-137">Hello SCP подключаемого модуля записи просто Здравствуйте, то же, что записи любые другие стандартные приложения консоли Windows.</span><span class="sxs-lookup"><span data-stu-id="71ed0-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="71ed0-138">Платформа SCP.NET объявляет интерфейс для spout/молнии и эти интерфейсы следует реализовывать hello пользовательского подключаемого модуля кода.</span><span class="sxs-lookup"><span data-stu-id="71ed0-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="71ed0-139">главной задачей Hello этой конструкции является этот пользователь hello позволяет сосредоточиться на своих собственных бизнес-логики и оставляя toobe другие вещи, обрабатываемых SCP.NET платформы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="71ed0-140">Hello пользовательского подключаемого модуля кода должен реализовывать один из интерфейсов hello следующие действия, зависит ли топологии hello транзакционной или нетранзакционной, и является ли компонент hello spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="71ed0-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="71ed0-141">ISCPSpout</span></span>
* <span data-ttu-id="71ed0-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="71ed0-142">ISCPBolt</span></span>
* <span data-ttu-id="71ed0-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="71ed0-143">ISCPTxSpout</span></span>
* <span data-ttu-id="71ed0-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="71ed0-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="71ed0-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="71ed0-145">ISCPPlugin</span></span>
<span data-ttu-id="71ed0-146">ISCPPlugin — hello общий интерфейс для всех видов подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="71ed0-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="71ed0-147">В данном случае мы работаем с имитатором интерфейса.</span><span class="sxs-lookup"><span data-stu-id="71ed0-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="71ed0-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="71ed0-148">ISCPSpout</span></span>
<span data-ttu-id="71ed0-149">ISCPSpout является интерфейсом hello для нетранзакционных spout.</span><span class="sxs-lookup"><span data-stu-id="71ed0-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="71ed0-150">Когда `NextTuple()` вызывается hello C\# пользовательский код можно создавать один или несколько раз.</span><span class="sxs-lookup"><span data-stu-id="71ed0-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="71ed0-151">Если нет ничего tooemit, этот метод должен возвращать без передачи ничего.</span><span class="sxs-lookup"><span data-stu-id="71ed0-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="71ed0-152">Нужно отметить, что команды `NextTuple()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#.</span><span class="sxs-lookup"><span data-stu-id="71ed0-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="71ed0-153">При наличии не tooemit кортежей, — спящий режим NextTuple вежливость toohave для за короткий промежуток времени (например, 10 миллисекунд), поскольку не toowaste чрезмерно загружающих ЦП.</span><span class="sxs-lookup"><span data-stu-id="71ed0-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="71ed0-154">Команды `Ack()` и `Fail()` вызываются только в случае активации механизма подтверждения в файле спецификации.</span><span class="sxs-lookup"><span data-stu-id="71ed0-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="71ed0-155">Hello `seqId` представляет кортеж используется tooidentify hello, или не удалось выполнить запись.</span><span class="sxs-lookup"><span data-stu-id="71ed0-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="71ed0-156">Поэтому если ack включен нетранзакционный топологии, следует использовать после выдачи функции hello в Spout:</span><span class="sxs-lookup"><span data-stu-id="71ed0-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="71ed0-157">Здравствуйте, если ack не поддерживается в топологии нетранзакционной, `Ack()` и `Fail()` можно оставить пустым функции.</span><span class="sxs-lookup"><span data-stu-id="71ed0-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="71ed0-158">Hello `parms` входные параметры в эти функции являются просто пустой словарь, они зарезервированы для будущего использования.</span><span class="sxs-lookup"><span data-stu-id="71ed0-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="71ed0-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="71ed0-159">ISCPBolt</span></span>
<span data-ttu-id="71ed0-160">ISCPBolt является интерфейсом hello для нетранзакционных молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="71ed0-161">Если доступен новый кортежа, hello `Execute()` функция будет вызываться tooprocess его.</span><span class="sxs-lookup"><span data-stu-id="71ed0-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="71ed0-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="71ed0-162">ISCPTxSpout</span></span>
<span data-ttu-id="71ed0-163">ISCPTxSpout является интерфейсом hello для spout транзакций.</span><span class="sxs-lookup"><span data-stu-id="71ed0-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="71ed0-164">Так же как и в случае с нетранзакционными воронками, команды `NextTx()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#.</span><span class="sxs-lookup"><span data-stu-id="71ed0-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="71ed0-165">При наличии tooemit нет данных, он используется вежливость toohave `NextTx` спящий режим на короткий период времени (10 миллисекунд), поскольку не toowaste чрезмерно загружающих ЦП.</span><span class="sxs-lookup"><span data-stu-id="71ed0-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="71ed0-166">`NextTx()`вызывается toostart новую транзакцию, hello выходной параметр `seqId` транзакция используется tooidentify hello, используемый в `Ack()` и `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="71ed0-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="71ed0-167">В `NextTx()`, пользователя можно создавать стороне tooJava данных.</span><span class="sxs-lookup"><span data-stu-id="71ed0-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="71ed0-168">Hello данные будут храниться в ZooKeeper toosupport воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="71ed0-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="71ed0-169">Поскольку hello емкости ZooKeeper не ограничены, пользователя только должны предоставлять метаданные, не массового данных транзакций spout.</span><span class="sxs-lookup"><span data-stu-id="71ed0-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="71ed0-170">Storm автоматически повторит транзакцию, если она завершилась с ошибкой, поэтому в нормальных условиях `Fail()` вызывать не следует.</span><span class="sxs-lookup"><span data-stu-id="71ed0-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="71ed0-171">Но если точка подключения службы можно проверить метаданные hello, генерируемой транзакций spout, оно может вызвать `Fail()` при hello метаданные являются недопустимыми.</span><span class="sxs-lookup"><span data-stu-id="71ed0-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="71ed0-172">Hello `parms` входные параметры в эти функции являются просто пустой словарь, они зарезервированы для будущего использования.</span><span class="sxs-lookup"><span data-stu-id="71ed0-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="71ed0-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="71ed0-173">ISCPBatchBolt</span></span>
<span data-ttu-id="71ed0-174">ISCPBatchBolt является интерфейсом hello для транзакций молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="71ed0-175">`Execute()`вызывается при наличии нового кортежа, поступающих в hello молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="71ed0-176">`FinishBatch()` вызывается после завершения этой транзакции.</span><span class="sxs-lookup"><span data-stu-id="71ed0-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="71ed0-177">Hello `parms` входной параметр зарезервирован для будущего использования.</span><span class="sxs-lookup"><span data-stu-id="71ed0-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="71ed0-178">Для транзакционной топологии существует важная концепция — `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="71ed0-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="71ed0-179">Она содержит два поля: `TxId` и `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="71ed0-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="71ed0-180">`TxId`является используется tooidentify определенной транзакции, и для данной транзакции может существовать несколько попыток при сбое транзакции hello воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="71ed0-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="71ed0-181">SCP.NET новые будет другой ISCPBatchBolt объекта tooprocess каждого `StormTxAttempt`точно так же, как чего Storm стороне Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="71ed0-182">смысл этой конструкции Hello — toosupport обработки параллельных транзакций.</span><span class="sxs-lookup"><span data-stu-id="71ed0-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="71ed0-183">Пользователю необходимо учитывать его, если завершения попытки транзакции, соответствующего объекта ISCPBatchBolt hello будут уничтожены и сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="71ed0-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="71ed0-184">Объектная модель</span><span class="sxs-lookup"><span data-stu-id="71ed0-184">Object Model</span></span>
<span data-ttu-id="71ed0-185">SCP.NET также предоставляет простой набор ключевых объектов для разработчиков tooprogram с.</span><span class="sxs-lookup"><span data-stu-id="71ed0-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="71ed0-186">В их число входят: **Context**, **StateStore** и **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="71ed0-187">Они обсуждаются в hello остальной части этого раздела.</span><span class="sxs-lookup"><span data-stu-id="71ed0-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="71ed0-188">Context</span><span class="sxs-lookup"><span data-stu-id="71ed0-188">Context</span></span>
<span data-ttu-id="71ed0-189">Контекст предоставляет работающее приложение toohello среды.</span><span class="sxs-lookup"><span data-stu-id="71ed0-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="71ed0-190">Каждому экземпляру дополнительного модуля ISCP (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) соответствует экземпляр объекта Context.</span><span class="sxs-lookup"><span data-stu-id="71ed0-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="71ed0-191">Hello функциональные возможности, предоставляемые контекст можно разделить на две части: статическую часть hello (1), которое доступно в hello всей C\# обработки динамической части hello (2), который доступен только для конкретного экземпляра контекстного hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="71ed0-192">Статическая часть</span><span class="sxs-lookup"><span data-stu-id="71ed0-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="71ed0-193">`Logger` отвечает за создание записей в журнале.</span><span class="sxs-lookup"><span data-stu-id="71ed0-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="71ed0-194">`pluginType`— используется тип подключаемого модуля hello tooindicate hello C\# процесса.</span><span class="sxs-lookup"><span data-stu-id="71ed0-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="71ed0-195">Если hello C\# процесс выполняется в локальном режиме (без Java), тип подключаемого модуля hello `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="71ed0-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="71ed0-196">`Config`предоставляется tooget параметры конфигурации со стороны Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="71ed0-197">Hello параметры передаются со стороны Java при C\# инициализации подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="71ed0-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="71ed0-198">Hello `Config` параметры делятся на две части: `stormConf` и `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="71ed0-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="71ed0-199">`stormConf`— параметров, определенных Storm и `pluginConf` — hello параметров, определенных точка подключения службы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="71ed0-200">Например:</span><span class="sxs-lookup"><span data-stu-id="71ed0-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="71ed0-201">`TopologyContext`предоставляется tooget hello топологии контекста, это может пригодиться, для компонентов с несколькими параллелизма.</span><span class="sxs-lookup"><span data-stu-id="71ed0-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="71ed0-202">Пример:</span><span class="sxs-lookup"><span data-stu-id="71ed0-202">Here is an example:</span></span>

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

### <a name="dynamic-part"></a><span data-ttu-id="71ed0-203">Динамическая часть</span><span class="sxs-lookup"><span data-stu-id="71ed0-203">Dynamic Part</span></span>
<span data-ttu-id="71ed0-204">Здравствуйте, следующие интерфейсы являются нужные tooa экземпляром определенного контекста.</span><span class="sxs-lookup"><span data-stu-id="71ed0-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="71ed0-205">экземпляр контекста Hello создается платформой SCP.NET и передается toohello пользовательского кода:</span><span class="sxs-lookup"><span data-stu-id="71ed0-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="71ed0-206">Для поддержки ack нетранзакционных spout предоставляется hello следующий метод:</span><span class="sxs-lookup"><span data-stu-id="71ed0-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="71ed0-207">Для нетранзакционных молнии поддержки ack, должны явным образом `Ack()` или `Fail()` hello кортежа, оно получено.</span><span class="sxs-lookup"><span data-stu-id="71ed0-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="71ed0-208">А при выдаче нового кортежа, его необходимо задать привязки hello hello новый кортежа.</span><span class="sxs-lookup"><span data-stu-id="71ed0-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="71ed0-209">предоставляются следующие методы Hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="71ed0-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="71ed0-210">StateStore</span></span>
<span data-ttu-id="71ed0-211">`StateStore` предоставляет службы метаданных, создание монотонных последовательностей и координацию без ожидания.</span><span class="sxs-lookup"><span data-stu-id="71ed0-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="71ed0-212">Распределенные многозадачные абстракции высокого уровня могут создаваться на базе `StateStore`, включая создание распределенных блокировок, распределенных очередей, барьеров и служб транзакций.</span><span class="sxs-lookup"><span data-stu-id="71ed0-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="71ed0-213">Точка подключения службы приложения могут использовать hello `State` объекта toopersist некоторые сведения в ZooKeeper, особенно для транзакционной топологии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="71ed0-214">. Таким образом, если транзакций spout аварийно завершает работу и перезапустите, он мог получить необходимую информацию hello из ZooKeeper и перезапустите hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="71ed0-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="71ed0-215">Hello `StateStore` объекта в основном включает следующие методы:</span><span class="sxs-lookup"><span data-stu-id="71ed0-215">hello `StateStore` object mainly has these methods:</span></span>

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

<span data-ttu-id="71ed0-216">Hello `State` объекта в основном включает следующие методы:</span><span class="sxs-lookup"><span data-stu-id="71ed0-216">hello `State` object mainly has these methods:</span></span>

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

<span data-ttu-id="71ed0-217">Для hello `Commit()` при метод simpleMode задано tootrue, он просто удалит соответствующие ZNode в ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="71ed0-218">В противном случае он будет удален текущий ZNode hello и Добавление нового узла в hello ЗАФИКСИРОВАНО\_пути.</span><span class="sxs-lookup"><span data-stu-id="71ed0-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="71ed0-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="71ed0-219">SCPRuntime</span></span>
<span data-ttu-id="71ed0-220">SCPRuntime предоставляет следующие два метода hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="71ed0-221">`Initialize()`Представляет среду выполнения используется tooinitialize hello точка подключения службы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="71ed0-222">В этом методе hello C\# процесс будет подключаться стороне toohello Java и возвращает параметры конфигурации и топологии контекста.</span><span class="sxs-lookup"><span data-stu-id="71ed0-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="71ed0-223">`LaunchPlugin()`используется tookick off приветственное сообщение, обрабатывает цикла.</span><span class="sxs-lookup"><span data-stu-id="71ed0-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="71ed0-224">В этом цикле hello C\# подключаемого модуля, получат сообщения форму стороны Java (включая кортежей и сигналов управления), а затем обрабатывать сообщения hello, может быть вызов метода интерфейса hello укажите с помощью пользовательского кода hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="71ed0-225">Hello входного параметра для метода `LaunchPlugin()` является делегатом, который может возвращать объект, который реализует интерфейс ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="71ed0-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="71ed0-226">Для ISCPBatchBolt, мы можем получить `StormTxAttempt` из `parms`и использовать его toojudge, будь то воспроизводимой попытки.</span><span class="sxs-lookup"><span data-stu-id="71ed0-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="71ed0-227">Обычно это делается на молнии фиксации hello и демонстрируется hello `HelloWorldTx` примере.</span><span class="sxs-lookup"><span data-stu-id="71ed0-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="71ed0-228">Вообще говоря hello SCP подключаемые модули запускаются в двух режимах здесь:</span><span class="sxs-lookup"><span data-stu-id="71ed0-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="71ed0-229">Локальный режим теста: В этом режиме hello SCP подключаемых модулей (hello C\# пользовательского кода) выполняются в Visual Studio на этапе разработки hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="71ed0-230">`LocalContext`может использоваться в этом режиме, который предоставляет метод tooserialize hello создается кортежей toolocal файлов и чтение их откат toomemory.</span><span class="sxs-lookup"><span data-stu-id="71ed0-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="71ed0-231">Обычный режим: В этом режиме подключаемых модулей SCP hello запущенных процессом java storm.</span><span class="sxs-lookup"><span data-stu-id="71ed0-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="71ed0-232">Ниже дан пример запуска дополнительного модуля SCP:</span><span class="sxs-lookup"><span data-stu-id="71ed0-232">Here is an example of launching SCP plugin:</span></span>
   
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

## <a name="topology-specification-language"></a><span data-ttu-id="71ed0-233">Язык спецификации топологии</span><span class="sxs-lookup"><span data-stu-id="71ed0-233">Topology Specification Language</span></span>
<span data-ttu-id="71ed0-234">Спецификация топологии SCP представляет собой специализированный язык для описания и настройки топологий SCP.</span><span class="sxs-lookup"><span data-stu-id="71ed0-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="71ed0-235">Он основан на Clojure DSL для Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) и расширен с помощью SCP.</span><span class="sxs-lookup"><span data-stu-id="71ed0-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="71ed0-236">Спецификации топологии, которые можно отправить непосредственно toostorm кластера для выполнения через hello ***runspec*** команды.</span><span class="sxs-lookup"><span data-stu-id="71ed0-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="71ed0-237">SCP.NET имеет добавить следующие функции toodefine hello транзакций топологии:</span><span class="sxs-lookup"><span data-stu-id="71ed0-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="71ed0-238">**Новые функции**</span><span class="sxs-lookup"><span data-stu-id="71ed0-238">**New Functions**</span></span> | <span data-ttu-id="71ed0-239">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="71ed0-239">**Parameters**</span></span> | <span data-ttu-id="71ed0-240">**Описание**</span><span class="sxs-lookup"><span data-stu-id="71ed0-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71ed0-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="71ed0-241">**tx-topolopy**</span></span> |<span data-ttu-id="71ed0-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-242">topology-name</span></span><br /><span data-ttu-id="71ed0-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="71ed0-243">spout-map</span></span><br /><span data-ttu-id="71ed0-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="71ed0-244">bolt-map</span></span> |<span data-ttu-id="71ed0-245">Определение топологии транзакций с именем hello топологии, &nbsp;spouts определения карты и карты определение винты hello</span><span class="sxs-lookup"><span data-stu-id="71ed0-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="71ed0-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="71ed0-246">**scp-tx-spout**</span></span> |<span data-ttu-id="71ed0-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-247">exec-name</span></span><br /><span data-ttu-id="71ed0-248">args</span><span class="sxs-lookup"><span data-stu-id="71ed0-248">args</span></span><br /><span data-ttu-id="71ed0-249">fields</span><span class="sxs-lookup"><span data-stu-id="71ed0-249">fields</span></span> |<span data-ttu-id="71ed0-250">Определение транзакционной "воронки".</span><span class="sxs-lookup"><span data-stu-id="71ed0-250">Define a transactional spout.</span></span> <span data-ttu-id="71ed0-251">Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.</span><span class="sxs-lookup"><span data-stu-id="71ed0-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="71ed0-252">Hello ***поля*** является hello выходные данные поля для spout</span><span class="sxs-lookup"><span data-stu-id="71ed0-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="71ed0-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="71ed0-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="71ed0-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-254">exec-name</span></span><br /><span data-ttu-id="71ed0-255">args</span><span class="sxs-lookup"><span data-stu-id="71ed0-255">args</span></span><br /><span data-ttu-id="71ed0-256">fields</span><span class="sxs-lookup"><span data-stu-id="71ed0-256">fields</span></span> |<span data-ttu-id="71ed0-257">Определение транзакционного пакетного "сита".</span><span class="sxs-lookup"><span data-stu-id="71ed0-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="71ed0-258">Он будет выполняться приложение hello с ***exec имя*** с помощью ***args.***</span><span class="sxs-lookup"><span data-stu-id="71ed0-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="71ed0-259">Hello поля — hello вывод полей для молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="71ed0-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="71ed0-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="71ed0-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-261">exec-name</span></span><br /><span data-ttu-id="71ed0-262">args</span><span class="sxs-lookup"><span data-stu-id="71ed0-262">args</span></span><br /><span data-ttu-id="71ed0-263">fields</span><span class="sxs-lookup"><span data-stu-id="71ed0-263">fields</span></span> |<span data-ttu-id="71ed0-264">Определение транзакционного подтверждающего "сита"</span><span class="sxs-lookup"><span data-stu-id="71ed0-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="71ed0-265">Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.</span><span class="sxs-lookup"><span data-stu-id="71ed0-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="71ed0-266">Hello ***поля*** — hello вывод полей для молнии</span><span class="sxs-lookup"><span data-stu-id="71ed0-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="71ed0-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="71ed0-267">**nontx-topolopy**</span></span> |<span data-ttu-id="71ed0-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-268">topology-name</span></span><br /><span data-ttu-id="71ed0-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="71ed0-269">spout-map</span></span><br /><span data-ttu-id="71ed0-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="71ed0-270">bolt-map</span></span> |<span data-ttu-id="71ed0-271">Определение топологии нетранзакционной с именем hello топологии,&nbsp; spouts определения карты и карты определение винты hello</span><span class="sxs-lookup"><span data-stu-id="71ed0-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="71ed0-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="71ed0-272">**scp-spout**</span></span> |<span data-ttu-id="71ed0-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-273">exec-name</span></span><br /><span data-ttu-id="71ed0-274">args</span><span class="sxs-lookup"><span data-stu-id="71ed0-274">args</span></span><br /><span data-ttu-id="71ed0-275">fields</span><span class="sxs-lookup"><span data-stu-id="71ed0-275">fields</span></span><br /><span data-ttu-id="71ed0-276">parameters</span><span class="sxs-lookup"><span data-stu-id="71ed0-276">parameters</span></span> |<span data-ttu-id="71ed0-277">Определение нетранзакционной "воронки".</span><span class="sxs-lookup"><span data-stu-id="71ed0-277">Define a nontransactional spout.</span></span> <span data-ttu-id="71ed0-278">Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.</span><span class="sxs-lookup"><span data-stu-id="71ed0-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="71ed0-279">Hello ***поля*** является hello выходные данные поля для spout</span><span class="sxs-lookup"><span data-stu-id="71ed0-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="71ed0-280">Hello ***параметры*** является необязательным, с помощью toospecify некоторые параметры, такие как «nontransactional.ack.enabled».</span><span class="sxs-lookup"><span data-stu-id="71ed0-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="71ed0-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="71ed0-281">**scp-bolt**</span></span> |<span data-ttu-id="71ed0-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="71ed0-282">exec-name</span></span><br /><span data-ttu-id="71ed0-283">args</span><span class="sxs-lookup"><span data-stu-id="71ed0-283">args</span></span><br /><span data-ttu-id="71ed0-284">fields</span><span class="sxs-lookup"><span data-stu-id="71ed0-284">fields</span></span><br /><span data-ttu-id="71ed0-285">parameters</span><span class="sxs-lookup"><span data-stu-id="71ed0-285">parameters</span></span> |<span data-ttu-id="71ed0-286">Определение нетранзакционного "сита".</span><span class="sxs-lookup"><span data-stu-id="71ed0-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="71ed0-287">Он будет выполняться приложение hello с ***exec имя*** с помощью ***args***.</span><span class="sxs-lookup"><span data-stu-id="71ed0-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="71ed0-288">Hello ***поля*** — hello вывод полей для молнии</span><span class="sxs-lookup"><span data-stu-id="71ed0-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="71ed0-289">Hello ***параметры*** является необязательным, с помощью toospecify некоторые параметры, такие как «nontransactional.ack.enabled».</span><span class="sxs-lookup"><span data-stu-id="71ed0-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="71ed0-290">Для SCP.NET определены следующие ключевые слова:</span><span class="sxs-lookup"><span data-stu-id="71ed0-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="71ed0-291">**Ключевые слова**</span><span class="sxs-lookup"><span data-stu-id="71ed0-291">**Key Words**</span></span> | <span data-ttu-id="71ed0-292">**Описание**</span><span class="sxs-lookup"><span data-stu-id="71ed0-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="71ed0-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="71ed0-293">**:name**</span></span> |<span data-ttu-id="71ed0-294">Определите имя топологии hello</span><span class="sxs-lookup"><span data-stu-id="71ed0-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="71ed0-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="71ed0-295">**:topology**</span></span> |<span data-ttu-id="71ed0-296">Определение топологии с помощью hello выше функции hello и сборку в коллекции.</span><span class="sxs-lookup"><span data-stu-id="71ed0-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="71ed0-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="71ed0-297">**:p**</span></span> |<span data-ttu-id="71ed0-298">Определите hello указание параллелизма для каждого spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="71ed0-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="71ed0-299">**:config**</span></span> |<span data-ttu-id="71ed0-300">Определите настройки параметра или обновление hello существующих</span><span class="sxs-lookup"><span data-stu-id="71ed0-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="71ed0-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="71ed0-301">**:schema**</span></span> |<span data-ttu-id="71ed0-302">Определите hello схемы потока.</span><span class="sxs-lookup"><span data-stu-id="71ed0-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="71ed0-303">И часто используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="71ed0-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="71ed0-304">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="71ed0-304">**Parameter**</span></span> | <span data-ttu-id="71ed0-305">**Описание**</span><span class="sxs-lookup"><span data-stu-id="71ed0-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="71ed0-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="71ed0-306">**"plugin.name"**</span></span> |<span data-ttu-id="71ed0-307">Имя файла EXE-файл подключаемого модуля hello C#</span><span class="sxs-lookup"><span data-stu-id="71ed0-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="71ed0-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="71ed0-308">**"plugin.args"**</span></span> |<span data-ttu-id="71ed0-309">Аргументы параметров дополнительного модуля</span><span class="sxs-lookup"><span data-stu-id="71ed0-309">plugin args</span></span> |
| <span data-ttu-id="71ed0-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="71ed0-310">**"output.schema"**</span></span> |<span data-ttu-id="71ed0-311">Схема вывода</span><span class="sxs-lookup"><span data-stu-id="71ed0-311">Output schema</span></span> |
| <span data-ttu-id="71ed0-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="71ed0-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="71ed0-313">Если подтверждение обработки для нетранзакционной топологии активно.</span><span class="sxs-lookup"><span data-stu-id="71ed0-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="71ed0-314">Команда runspec Hello будут развернуты вместе с hello bits, использование hello как:</span><span class="sxs-lookup"><span data-stu-id="71ed0-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="71ed0-315">Hello ***ресурсов dir*** параметр является необязательным, вы должны toospecify его при необходимости tooplug C\# приложения и этот каталог будет содержать приложения hello, зависимости hello и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="71ed0-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="71ed0-316">Hello ***classpath*** также не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="71ed0-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="71ed0-317">Это используется toospecify hello Java classpath, если файл характеристик hello содержит Java Spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="71ed0-318">Прочие функции</span><span class="sxs-lookup"><span data-stu-id="71ed0-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="71ed0-319">Объявление схемы ввода и вывода</span><span class="sxs-lookup"><span data-stu-id="71ed0-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="71ed0-320">Hello пользователя может выдавать кортежа в языке C\# обработки, hello платформа должна tooserialize hello кортежа в byte [], передача tooJava стороне и Storm передаст этой цели toohello кортежа.</span><span class="sxs-lookup"><span data-stu-id="71ed0-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="71ed0-321">В то же время в нижестоящего компонента hello C\# процесс получения кортежа обратно стороне java и преобразовать исходные типы toohello платформой, все эти операции скрыты по hello платформы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="71ed0-322">toosupport hello сериализации и десериализации, пользовательский код должен схемы hello toodeclare hello входов и выходов.</span><span class="sxs-lookup"><span data-stu-id="71ed0-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="71ed0-323">Схема потока ввода вывода Hello определен как словарь hello ключом hello StreamId и hello значение — hello типы столбцов hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="71ed0-324">Hello компонент может иметь несколько потоков, которые объявлены.</span><span class="sxs-lookup"><span data-stu-id="71ed0-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="71ed0-325">В контексте объекта у нас есть hello добавлены следующие API:</span><span class="sxs-lookup"><span data-stu-id="71ed0-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="71ed0-326">Пользовательский код необходимо убедиться, создавшего кортежей hello подчиняются hello схемой, определенной для этого потока, либо hello система выдает исключение времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="71ed0-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="71ed0-327">Поддержка многопоточности</span><span class="sxs-lookup"><span data-stu-id="71ed0-327">Multi-Stream Support</span></span>
<span data-ttu-id="71ed0-328">Точка подключения службы поддерживает пользователя кода tooemit или получать из нескольких различных потоков в hello же время.</span><span class="sxs-lookup"><span data-stu-id="71ed0-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="71ed0-329">Поддержка Hello отражает hello объекта контекста как hello Emit метод принимает параметр ID дополнительный поток.</span><span class="sxs-lookup"><span data-stu-id="71ed0-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="71ed0-330">Были добавлены два метода в hello объекта SCP.NET контекста.</span><span class="sxs-lookup"><span data-stu-id="71ed0-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="71ed0-331">Они являются используется tooemit кортеж или кортежи toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="71ed0-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="71ed0-332">Hello StreamId — это строка, а также он должен toobe согласованность обоих C\# и hello Spec определения топологии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="71ed0-333">Hello выпускающей tooa несуществующего потока вызовут исключения среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="71ed0-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="71ed0-334">Группирование полей</span><span class="sxs-lookup"><span data-stu-id="71ed0-334">Fields Grouping</span></span>
<span data-ttu-id="71ed0-335">Hello сборки в группирование полей Strom работает неправильно в SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="71ed0-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="71ed0-336">На hello стороны Java прокси-сервера все типы данных полей hello, фактически byte [] и группирование полей hello использует hello byte [] объекта хэша кода tooperform hello группирования.</span><span class="sxs-lookup"><span data-stu-id="71ed0-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="71ed0-337">хэш-код byte [] Hello объекта — адрес hello объекта в памяти.</span><span class="sxs-lookup"><span data-stu-id="71ed0-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="71ed0-338">Таким образом, группирование hello неправильный для двух байтов [] объектов этой общей папке hello же содержимого, но не hello того же адреса.</span><span class="sxs-lookup"><span data-stu-id="71ed0-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="71ed0-339">SCP.NET добавляет метод настроенные группирования и будет использовать содержимое hello hello byte [] toodo hello группирования.</span><span class="sxs-lookup"><span data-stu-id="71ed0-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="71ed0-340">В **SPEC** файл, синтаксис hello содержит:</span><span class="sxs-lookup"><span data-stu-id="71ed0-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="71ed0-341">В данном случае</span><span class="sxs-lookup"><span data-stu-id="71ed0-341">Here,</span></span>

1. <span data-ttu-id="71ed0-342">"scp-field-group" означает "адаптированный метод группирования полей с помощью SCP".</span><span class="sxs-lookup"><span data-stu-id="71ed0-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="71ed0-343">":tx" или "non-tx" означает транзакционную или нетранзакционную топологию.</span><span class="sxs-lookup"><span data-stu-id="71ed0-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="71ed0-344">Мы должны эти сведения, поскольку hello начальным индексом и топологии не tx отличается в tx.</span><span class="sxs-lookup"><span data-stu-id="71ed0-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="71ed0-345">[0,1] означает набор хэш-функций идентификаторов полей (начальное значение = "0").</span><span class="sxs-lookup"><span data-stu-id="71ed0-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="71ed0-346">Гибридная топология</span><span class="sxs-lookup"><span data-stu-id="71ed0-346">Hybrid topology</span></span>
<span data-ttu-id="71ed0-347">машинный код Hello Storm написан на языке Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="71ed0-348">И SCP.Net усовершенствованы его tooenable нашей правил toowrite C\# кода toohandle их бизнес-логике.</span><span class="sxs-lookup"><span data-stu-id="71ed0-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="71ed0-349">Но мы также поддерживаем гибридные топологии, в которых воронки и сита возможны не только на C\#, но и на Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="71ed0-350">Задание "воронок" и "сит" на Java в файле спецификаций.</span><span class="sxs-lookup"><span data-stu-id="71ed0-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="71ed0-351">В спецификации файла «scp spout» и «scp молнии» также можно использовать toospecify Spouts Java и винты, ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="71ed0-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="71ed0-352">Здесь `microsoft.scp.example.HybridTopology.Generator` — имя hello hello Java Spout класса.</span><span class="sxs-lookup"><span data-stu-id="71ed0-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="71ed0-353">Указание classpath Java в команде runSpec</span><span class="sxs-lookup"><span data-stu-id="71ed0-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="71ed0-354">Следует toosubmit топологии, содержащий Java Spouts или винты требуется hello компиляции toofirst Java Spouts или винты и получить hello Jar-файла.</span><span class="sxs-lookup"><span data-stu-id="71ed0-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="71ed0-355">Необходимо указать hello java classpath, содержащий hello Jar-файла при отправке топологии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="71ed0-356">Пример:</span><span class="sxs-lookup"><span data-stu-id="71ed0-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="71ed0-357">Здесь **примеры\\HybridTopology\\java\\целевой\\**  hello папку, содержащую файл Jar Spout/молнии Java hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="71ed0-358">Сериализация или десериализация между Java и C#</span><span class="sxs-lookup"><span data-stu-id="71ed0-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="71ed0-359">Компонент SCP включает в себя часть C\# и часть Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="71ed0-360">В порядке toointeract с собственного Java Spouts/винты, сериализации и десериализации должно быть выполнено между границей Java и C\# стороны, как показано в следующих graph hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![Схема отправки tooSCP компонента отправки компонент tooJava компонента java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="71ed0-362">**Сериализация на стороне Java и десериализация на стороне C\#**</span><span class="sxs-lookup"><span data-stu-id="71ed0-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="71ed0-363">Для начала нужно обеспечить стандартное применение сериализации на стороне Java и десериализации на стороне C\#.</span><span class="sxs-lookup"><span data-stu-id="71ed0-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="71ed0-364">метод сериализации Hello в сторону Java можно указать в файле характеристик:</span><span class="sxs-lookup"><span data-stu-id="71ed0-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="71ed0-365">Здравствуйте, метод десериализации в языке C\# стороны должно быть указано в C\# пользовательского кода:</span><span class="sxs-lookup"><span data-stu-id="71ed0-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="71ed0-366">Данная реализация по умолчанию должен обрабатывать большинстве случаев, если тип данных hello не является слишком сложным.</span><span class="sxs-lookup"><span data-stu-id="71ed0-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="71ed0-367">В некоторых случаях либо поскольку hello пользовательского типа данных является слишком сложным или hello производительность реализацию по умолчанию не соответствует hello требований пользователя, пользователь может подключаемый модуль свою собственную реализацию.</span><span class="sxs-lookup"><span data-stu-id="71ed0-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="71ed0-368">интерфейс сериализации Hello в java стороны определяется как:</span><span class="sxs-lookup"><span data-stu-id="71ed0-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="71ed0-369">Hello десериализации интерфейса в C\# стороне определяется как:</span><span class="sxs-lookup"><span data-stu-id="71ed0-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="71ed0-370">Общедоступный интерфейс ICustomizedInteropCSharpDeserializer.</span><span class="sxs-lookup"><span data-stu-id="71ed0-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="71ed0-371">**Сериализация на стороне C\# и десериализация на стороне Java**</span><span class="sxs-lookup"><span data-stu-id="71ed0-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="71ed0-372">Здравствуйте, метод сериализации в C\# стороны должно быть указано в C\# пользовательского кода:</span><span class="sxs-lookup"><span data-stu-id="71ed0-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="71ed0-373">метод десериализации стороне Java Hello должно быть указано в СПЕЦИФИКАЦИИ файла:</span><span class="sxs-lookup"><span data-stu-id="71ed0-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="71ed0-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="71ed0-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="71ed0-375">Вот десериализатор hello имя «microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer» и «microsoft.scp.example.HybridTopology.Person» — для десериализации класса hello hello целевых данных.</span><span class="sxs-lookup"><span data-stu-id="71ed0-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="71ed0-376">Пользователь может также подключить свою собственную реализацию сериализатора C\# и десериализатора Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="71ed0-377">Это интерфейс hello для C\# сериализатор:</span><span class="sxs-lookup"><span data-stu-id="71ed0-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="71ed0-378">Это интерфейс hello для десериализатор Java:</span><span class="sxs-lookup"><span data-stu-id="71ed0-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="71ed0-379">Хост-режим SCP</span><span class="sxs-lookup"><span data-stu-id="71ed0-379">SCP Host Mode</span></span>
<span data-ttu-id="71ed0-380">В этом режиме пользователь можно скомпилировать их tooDLL коды и использовать SCPHost.exe предоставляемые SCP toosubmit топологии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="71ed0-381">Спецификация файла Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="71ed0-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="71ed0-382">Здесь в качестве `plugin.name` указан `SCPHost.exe` из пакета SDK для SCP.</span><span class="sxs-lookup"><span data-stu-id="71ed0-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="71ed0-383">SCPHost.exe принимает только три параметра:</span><span class="sxs-lookup"><span data-stu-id="71ed0-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="71ed0-384">Hello сначала он hello DLL имя, являющееся `"HelloWorld.dll"` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="71ed0-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="71ed0-385">Hello второе — это имя класса hello, являющееся `"Scp.App.HelloWorld.Generator"` в этом примере.</span><span class="sxs-lookup"><span data-stu-id="71ed0-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="71ed0-386">Hello третий он hello имени общего статического метода, который может быть вызванным tooget экземпляр ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="71ed0-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="71ed0-387">В хост-режиме код пользователя компилируется в DLL-файл и вызывается платформой SCP.</span><span class="sxs-lookup"><span data-stu-id="71ed0-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="71ed0-388">Поэтому SCP платформы можно получить полный контроль над логику обработки всей hello.</span><span class="sxs-lookup"><span data-stu-id="71ed0-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="71ed0-389">Поэтому рекомендуется наших клиентов toosubmit топологии в режиме SCP узла, так как его можно упростить процесс разработки hello и расскажи нам большую гибкость и лучше обратной совместимости для более поздней версии также.</span><span class="sxs-lookup"><span data-stu-id="71ed0-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="71ed0-390">Примеры программирования для SCP</span><span class="sxs-lookup"><span data-stu-id="71ed0-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="71ed0-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="71ed0-391">HelloWorld</span></span>
<span data-ttu-id="71ed0-392">**HelloWorld** является tooshow очень простой пример, чтобы получить представление о SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="71ed0-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="71ed0-393">Она использует нетранзакционную топологию, в которой воронка называется **generator**, а два сита — **splitter** и **counter**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="71ed0-394">Hello spout **генератор** будет случайным образом создать некоторые предложения и передачи этих предложений слишком**разделителей**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="71ed0-395">Hello молнии **разделителей** будет разделить toowords предложений hello и создавать эти слова слишком**счетчика** молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="71ed0-396">Hello молнии «счетчик» используется ряд словарь hello toorecord вхождения каждого слова.</span><span class="sxs-lookup"><span data-stu-id="71ed0-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="71ed0-397">Для этого примера существует два файла спецификации — **HelloWorld.spec** и **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="71ed0-398">В hello C\# кода, его можно узнать включении ack, обратившись hello pluginConf со стороны Java.</span><span class="sxs-lookup"><span data-stu-id="71ed0-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="71ed0-399">При включении ack словарь в hello spout является используется toocache hello кортежей, которые не были запись.</span><span class="sxs-lookup"><span data-stu-id="71ed0-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="71ed0-400">При вызове Fail() hello неудачных кортеж будет воспроизведен в:</span><span class="sxs-lookup"><span data-stu-id="71ed0-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

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

### <a name="helloworldtx"></a><span data-ttu-id="71ed0-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="71ed0-401">HelloWorldTx</span></span>
<span data-ttu-id="71ed0-402">Hello **HelloWorldTx** примере показано, как tooimplement транзакций топологии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="71ed0-403">В ней воронка называется **generator**, пакетные сита — **partial-count**, а подтверждающее сито — **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="71ed0-404">В примере содержатся три предварительно созданных текстовых файла: **DataSource0.txt**, **DataSource1.txt** и **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="71ed0-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="71ed0-405">В каждой транзакции hello spout **генератор** будет случайным образом выбрать два файла из ранее созданной три файла hello и передачи hello два файла имена toohello **частичного число** молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="71ed0-406">Hello молнии **частичного число** сначала нужно получить имя файла hello из полученных hello кортежа, а затем Привет открыть файл и число hello количество слов в этот файл и наконец порождение номеров toohello слово hello **счетчик сумма**молнии.</span><span class="sxs-lookup"><span data-stu-id="71ed0-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="71ed0-407">Hello **сумма число** молнии будут использованы Помесячные hello общее число объектов.</span><span class="sxs-lookup"><span data-stu-id="71ed0-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="71ed0-408">tooachieve **ровно один раз** семантику, молнии фиксации hello **сумма число** требуется toojudge, будь то воспроизводимой транзакции.</span><span class="sxs-lookup"><span data-stu-id="71ed0-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="71ed0-409">В этом примере транзакция имеет статическую переменную-член.</span><span class="sxs-lookup"><span data-stu-id="71ed0-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="71ed0-410">Когда создается экземпляр ISCPBatchBolt, он получит hello `txAttempt` из входных параметров:</span><span class="sxs-lookup"><span data-stu-id="71ed0-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

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

<span data-ttu-id="71ed0-411">Когда `FinishBatch()` вызове hello `lastCommittedTxId` будет обновления, если это не воспроизводимой транзакции.</span><span class="sxs-lookup"><span data-stu-id="71ed0-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

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


### <a name="hybridtopology"></a><span data-ttu-id="71ed0-412">Гибридная топология</span><span class="sxs-lookup"><span data-stu-id="71ed0-412">HybridTopology</span></span>
<span data-ttu-id="71ed0-413">Данная топология содержит воронку на Java и сито на C\#.</span><span class="sxs-lookup"><span data-stu-id="71ed0-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="71ed0-414">Она использует hello реализация по умолчанию сериализации и десериализации SCP платформы.</span><span class="sxs-lookup"><span data-stu-id="71ed0-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="71ed0-415">Пожалуйста, ref hello **HybridTopology.spec** в **примеры\\HybridTopology** папку hello характеристик сведений о файлах, и **SubmitTopology.bat** как toospecify Java classpath.</span><span class="sxs-lookup"><span data-stu-id="71ed0-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="71ed0-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="71ed0-416">SCPHostDemo</span></span>
<span data-ttu-id="71ed0-417">В этом примере hello аналогично HelloWorld в сущности.</span><span class="sxs-lookup"><span data-stu-id="71ed0-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="71ed0-418">Hello единственным отличием является hello пользовательский код компилируется как библиотеки DLL и топологии hello передается с помощью SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="71ed0-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="71ed0-419">Более подробные объяснения, перенесите ref hello раздел «Режим узла SCP».</span><span class="sxs-lookup"><span data-stu-id="71ed0-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71ed0-420">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71ed0-420">Next Steps</span></span>
<span data-ttu-id="71ed0-421">Примеры топологий Storm, созданных с помощью точки подключения службы см. в следующем hello:</span><span class="sxs-lookup"><span data-stu-id="71ed0-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="71ed0-422">Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71ed0-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="71ed0-423">Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71ed0-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="71ed0-424">Создание нескольких потоков данных в топологии Storm на C#</span><span class="sxs-lookup"><span data-stu-id="71ed0-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="71ed0-425">Использование Power Bi toovisualize данных из топологии Storm</span><span class="sxs-lookup"><span data-stu-id="71ed0-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="71ed0-426">Обработка данных с датчиков автомобиля из концентраторов событий с использованием Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71ed0-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="71ed0-427">Извлечения, преобразования и загрузки (ETL) из tooHBase концентраторов событий Azure</span><span class="sxs-lookup"><span data-stu-id="71ed0-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="71ed0-428">Сопоставление событий с помощью Storm и HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="71ed0-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

