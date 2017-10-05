---
title: "Руководство по программированию для SCP.NET | Документация Майкрософт"
description: "Узнайте, как использовать SCP.NET для создания топологий Storm на основе .NET для использования со Storm в HDInsight."
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
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="b60f7-103">Руководство по программированию для SCP</span><span class="sxs-lookup"><span data-stu-id="b60f7-103">SCP programming guide</span></span>
<span data-ttu-id="b60f7-104">SPC — это платформа для создания надежного, согласованного и высокопроизводительного приложения для обработки данных в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="b60f7-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="b60f7-105">Она основана на [Apache Storm](http://storm.incubator.apache.org/) — системе обработки потоковых данных, созданной сообществами разработчиков OSS.</span><span class="sxs-lookup"><span data-stu-id="b60f7-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="b60f7-106">Создателем Storm является Натан Марц (Nathan Marz), программа имеет открытый код и распространяется компанией Twitter.</span><span class="sxs-lookup"><span data-stu-id="b60f7-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="b60f7-107">В платформе используется [Apache ZooKeeper](http://zookeeper.apache.org/)— еще один проект Apache для обеспечения высоконадежной распределенной координации и управления состоянием.</span><span class="sxs-lookup"><span data-stu-id="b60f7-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="b60f7-108">С помощью проекта SPC удалось не только перенести Storm в Windows, но и добавить расширения и адаптировать его для работы в экосистеме Windows.</span><span class="sxs-lookup"><span data-stu-id="b60f7-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="b60f7-109">Дополнения включают в себя возможности разработки .NET и библиотеки; адаптация заключается в возможности развертывания на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="b60f7-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="b60f7-110">Дополнения и адаптация выполнены таким образом, что нам не придется разветвлять проекты OSS, а можно использовать производные экосистемы, созданные на базе Storm.</span><span class="sxs-lookup"><span data-stu-id="b60f7-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="b60f7-111">Модель обработки данных</span><span class="sxs-lookup"><span data-stu-id="b60f7-111">Processing model</span></span>
<span data-ttu-id="b60f7-112">Данные в SCP оформляются в виде постоянных потоков кортежей данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="b60f7-113">Обычно кортежи оформляются в виде очереди на первом этапе, затем бизнес-логика приложения, находящегося внутри топологии Storm, подбирает и трансформирует их. Наконец, данные на выходе могут подаваться в виде кортежей в другую систему SCP или отправляться на хранение в системы распределенных файлов или базы данных, например SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b60f7-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Схема очереди, передающей данные для обработки, которая наполняет хранилище данных](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="b60f7-115">В Storm вычислительные графы определяются топологией приложения.</span><span class="sxs-lookup"><span data-stu-id="b60f7-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="b60f7-116">Каждый узел в топологии содержит логическую схему обработки информации, а по связям между узлами можно определить движение потока данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="b60f7-117">Узлы, которые "вливают" входные данные в топологию, называются "воронками" (Spout) и могут использоваться для создания последовательности потока данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="b60f7-118">Входные данные могут располагаться в файлах журнала, транзакционной базе данных, системном счетчике производительности и т. д. Узлы для потоков входных и выходных данных называются "ситами", они осуществляют фактическую фильтрацию, и выбор и агрегацию данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="b60f7-119">SCP поддерживает максимальное качество работы при типе обработки данных "минимум однажды" и "только однажды".</span><span class="sxs-lookup"><span data-stu-id="b60f7-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="b60f7-120">В распределенном приложении для обработки потоковой передачи могут возникать различные ошибки во время обработки данных, например сбой сети, аппаратный сбой, ошибка в коде пользователя и т. п. Обработка по принципу "минимум однажды" гарантирует, что все данные будут обрабатываться по крайней мере один раз благодаря автоматической повторной обработке тех же данных в случае ошибки.</span><span class="sxs-lookup"><span data-stu-id="b60f7-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="b60f7-121">Модель обработки "только однажды" проста и надежна и отлично подходит для многих приложений.</span><span class="sxs-lookup"><span data-stu-id="b60f7-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="b60f7-122">Однако в случаях, когда приложение требует, например, точного подсчета данных, вид обработки "минимум однажды" недостаточен, поскольку одни и те же данные могут проходить через топологию приложения несколько раз.</span><span class="sxs-lookup"><span data-stu-id="b60f7-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="b60f7-123">Для подобных случаев разработан вид обработки "только однажды". Он обеспечивает достоверность итоговых данных даже в тех случаях, когда данные могут посылаться повторно и обрабатываться несколько раз подряд.</span><span class="sxs-lookup"><span data-stu-id="b60f7-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="b60f7-124">SCP позволяет разработчикам для .NET создавать приложения для обработки данных в реальном времени со скрытым использованием возможностей Storm на виртуальных машинах Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="b60f7-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="b60f7-125">.NET и JVM обмениваются данными через локальный TCP-сокет.</span><span class="sxs-lookup"><span data-stu-id="b60f7-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="b60f7-126">По сути, каждая пара "воронка/сито" — это пара процессов .Net/Java, в которой логика пользователя задействована в процессе .Net в качестве дополнительного модуля.</span><span class="sxs-lookup"><span data-stu-id="b60f7-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="b60f7-127">Для создания приложения для обработки данных поверх SCP необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="b60f7-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="b60f7-128">Создать и активировать "воронки" для извлечения данных из очереди.</span><span class="sxs-lookup"><span data-stu-id="b60f7-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="b60f7-129">Создать и активировать "сита" для обработки входящих данных и сохранения данных после обработки во внешнем хранилище, например в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="b60f7-130">Создать топологию процесса, загрузить и запустить ее.</span><span class="sxs-lookup"><span data-stu-id="b60f7-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="b60f7-131">Топология определяет вершины и поток данных между вершинами.</span><span class="sxs-lookup"><span data-stu-id="b60f7-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="b60f7-132">SCP получает спецификацию топологии и размещает из в кластере Storm, где каждая вершина работает в отдельном логическом узле.</span><span class="sxs-lookup"><span data-stu-id="b60f7-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="b60f7-133">Переход на резервный ресурс и масштабирование выполняет планировщик задач Storm.</span><span class="sxs-lookup"><span data-stu-id="b60f7-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="b60f7-134">В этой статье мы разберем несколько простых примеров создания приложения для обработки данных с помощью SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="b60f7-135">Интерфейс подключаемого модуля SCP</span><span class="sxs-lookup"><span data-stu-id="b60f7-135">SCP Plugin Interface</span></span>
<span data-ttu-id="b60f7-136">Дополнительные модули (или приложения) SCP — это автономные файлы типа EXE, которые можно запускать в Visual Studio во время фазы разработки, а также можно подключать к конвейеру Storm после завершения разработки.</span><span class="sxs-lookup"><span data-stu-id="b60f7-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="b60f7-137">Процесс написания кода дополнительного модуля SCP ничем не отличается от процессов написания кода для стандартных приложений в консоли Windows.</span><span class="sxs-lookup"><span data-stu-id="b60f7-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="b60f7-138">Платформа SCP.NET объявляет интерфейс для "воронки" и "сита", которые пользователю нужно заполнить программным кодом для модуля.</span><span class="sxs-lookup"><span data-stu-id="b60f7-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="b60f7-139">Это делается для того, чтобы пользователь мог сосредоточиться на своей задаче и предоставил платформе SCP.NET позаботиться обо всех остальных аспектах.</span><span class="sxs-lookup"><span data-stu-id="b60f7-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="b60f7-140">Код дополнительного модуля нужно внести в один из следующих интерфейсов, в зависимости от того, является ли топология транзакционной или нетранзакционной и является ли компонент "воронкой" или "ситом".</span><span class="sxs-lookup"><span data-stu-id="b60f7-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="b60f7-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b60f7-141">ISCPSpout</span></span>
* <span data-ttu-id="b60f7-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b60f7-142">ISCPBolt</span></span>
* <span data-ttu-id="b60f7-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b60f7-143">ISCPTxSpout</span></span>
* <span data-ttu-id="b60f7-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b60f7-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="b60f7-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="b60f7-145">ISCPPlugin</span></span>
<span data-ttu-id="b60f7-146">ISCPPlugin — это общий интерфейс для различных дополнительных модулей.</span><span class="sxs-lookup"><span data-stu-id="b60f7-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="b60f7-147">В данном случае мы работаем с имитатором интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b60f7-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="b60f7-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="b60f7-148">ISCPSpout</span></span>
<span data-ttu-id="b60f7-149">ISCPSpout — это интерфейс для нетранзакционных "воронок".</span><span class="sxs-lookup"><span data-stu-id="b60f7-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="b60f7-150">Когда вы вызываете `NextTuple()`, пользовательский код C\# может отправить один или несколько кортежей.</span><span class="sxs-lookup"><span data-stu-id="b60f7-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="b60f7-151">Если данных для отправки не существует, то возвращение метода должно произойти без отправки данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="b60f7-152">Нужно отметить, что команды `NextTuple()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b60f7-153">Если кортежей для отправки не существует, то разумно будет приостановить NextTuple на короткий промежуток времени (около 10 миллисекунд), чтобы излишне не нагружать ЦП.</span><span class="sxs-lookup"><span data-stu-id="b60f7-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="b60f7-154">Команды `Ack()` и `Fail()` вызываются только в случае активации механизма подтверждения в файле спецификации.</span><span class="sxs-lookup"><span data-stu-id="b60f7-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="b60f7-155">`seqId` используется для определения подтверждения или отклонения принятия кортежа.</span><span class="sxs-lookup"><span data-stu-id="b60f7-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="b60f7-156">Если подтверждение включено в нетранзакционной топологии, в "воронке" должны использоваться следующие функции отправки:</span><span class="sxs-lookup"><span data-stu-id="b60f7-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="b60f7-157">Если подтверждение не поддерживается нетранзакционной топологией, функции `Ack()` и `Fail()` можно не заполнять кодом.</span><span class="sxs-lookup"><span data-stu-id="b60f7-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="b60f7-158">Если входные параметры `parms` в этих функциях представляют собой пустой словарь, то их резервируют для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="b60f7-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="b60f7-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="b60f7-159">ISCPBolt</span></span>
<span data-ttu-id="b60f7-160">ISCPBolt — это интерфейс для нетранзакционных "сит"</span><span class="sxs-lookup"><span data-stu-id="b60f7-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="b60f7-161">При наличии нового кортежа для его обработки будет вызвана функция `Execute()` .</span><span class="sxs-lookup"><span data-stu-id="b60f7-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="b60f7-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="b60f7-162">ISCPTxSpout</span></span>
<span data-ttu-id="b60f7-163">ISCPTxSpout — это интерфейс для транзакционных "воронок".</span><span class="sxs-lookup"><span data-stu-id="b60f7-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="b60f7-164">Так же как и в случае с нетранзакционными воронками, команды `NextTx()`, `Ack()` и `Fail()` вызываются в сплошном цикле однопоточной обработки процесса C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="b60f7-165">Если данных для отправки не существует, то разумно будет приостановить `NextTx` на короткий промежуток времени (около 10 миллисекунд), чтобы излишне не нагружать ЦП.</span><span class="sxs-lookup"><span data-stu-id="b60f7-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="b60f7-166">`NextTx()` вызывается для того, чтобы начать новую передачу, для обозначения транзакции используется выходной параметр `seqId`, который также используется в командах `Ack()` и `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="b60f7-167">В случае с `NextTx()`пользователь может отправлять данные в часть Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="b60f7-168">Данные сохраняются в ZooKeeper для возможности провести повторную передачу.</span><span class="sxs-lookup"><span data-stu-id="b60f7-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="b60f7-169">Поскольку возможности хранения ZooKeeper ограничены, пользователи могут отправлять метаданные, но не могут отправлять данные большого объема в транзакционных "воронках".</span><span class="sxs-lookup"><span data-stu-id="b60f7-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="b60f7-170">Storm автоматически повторит транзакцию, если она завершилась с ошибкой, поэтому в нормальных условиях `Fail()` вызывать не следует.</span><span class="sxs-lookup"><span data-stu-id="b60f7-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="b60f7-171">Но так как платформа SCP может проверить метаданные от транзакционной "воронки", то она может вызвать `Fail()` , если метаданные неверны.</span><span class="sxs-lookup"><span data-stu-id="b60f7-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="b60f7-172">Если входные параметры `parms` в этих функциях представляют собой пустой словарь, то их резервируют для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="b60f7-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="b60f7-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="b60f7-173">ISCPBatchBolt</span></span>
<span data-ttu-id="b60f7-174">ISCPBatchBolt — это интерфейс для транзакционных "сит".</span><span class="sxs-lookup"><span data-stu-id="b60f7-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="b60f7-175">`Execute()` вызывается при наличии нового кортежа, поступающего в "сито".</span><span class="sxs-lookup"><span data-stu-id="b60f7-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="b60f7-176">`FinishBatch()` вызывается после завершения этой транзакции.</span><span class="sxs-lookup"><span data-stu-id="b60f7-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="b60f7-177">Входной параметр `parms` зарезервирован для использованию в будущем.</span><span class="sxs-lookup"><span data-stu-id="b60f7-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="b60f7-178">Для транзакционной топологии существует важная концепция — `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="b60f7-179">Она содержит два поля: `TxId` и `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="b60f7-180">`TxId` используется для определения специальной транзакции, и для заданной транзакции может предприниматься несколько попыток, если перед этим она завершилась ошибкой и была повторена.</span><span class="sxs-lookup"><span data-stu-id="b60f7-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="b60f7-181">SCP.NET создает отдельный объект ISCPBatchBolt для обработки `StormTxAttempt`, точно так же, как это делает Storm в части Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="b60f7-182">Это делается для поддержки параллельной обработки данных.</span><span class="sxs-lookup"><span data-stu-id="b60f7-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="b60f7-183">Пользователю необходимо помнить, что после завершения попытки передачи соответствующий объект ISCPBatchBolt будет уничтожен и удален как мусор.</span><span class="sxs-lookup"><span data-stu-id="b60f7-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="b60f7-184">Объектная модель</span><span class="sxs-lookup"><span data-stu-id="b60f7-184">Object Model</span></span>
<span data-ttu-id="b60f7-185">SCP.NET предоставляет разработчикам простой набор ключевых объектов для программирования.</span><span class="sxs-lookup"><span data-stu-id="b60f7-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="b60f7-186">В их число входят: **Context**, **StateStore** и **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="b60f7-187">О них пойдет речь в оставшейся части раздела.</span><span class="sxs-lookup"><span data-stu-id="b60f7-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="b60f7-188">Context</span><span class="sxs-lookup"><span data-stu-id="b60f7-188">Context</span></span>
<span data-ttu-id="b60f7-189">Context обеспечивает рабочую среду для приложений.</span><span class="sxs-lookup"><span data-stu-id="b60f7-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="b60f7-190">Каждому экземпляру дополнительного модуля ISCP (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) соответствует экземпляр объекта Context.</span><span class="sxs-lookup"><span data-stu-id="b60f7-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="b60f7-191">Функциональные возможности, предоставляемые Context, можно разделить на две части: статическая часть, доступная во всем процессе C\#, и динамическая часть, доступная только для определенного экземпляра Context.</span><span class="sxs-lookup"><span data-stu-id="b60f7-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="b60f7-192">Статическая часть</span><span class="sxs-lookup"><span data-stu-id="b60f7-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="b60f7-193">`Logger` отвечает за создание записей в журнале.</span><span class="sxs-lookup"><span data-stu-id="b60f7-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="b60f7-194">`pluginType` используется для указания типа подключаемого модуля в процессе C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="b60f7-195">Если процесс C`SCP_NET_LOCAL` запущен в локальном тестовом режиме (без Java), используется подключаемый модуль типа \#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="b60f7-196">`Config` предназначен для получения параметров конфигурации из части Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="b60f7-197">Параметры передаются со стороны Java после запуска подключаемого модуля на C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="b60f7-198">Параметры `Config` делятся на две части: `stormConf` и `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="b60f7-199">`stormConf` — это параметры, определенные Storm, а `pluginConf` — это параметры, определенные SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="b60f7-200">Например:</span><span class="sxs-lookup"><span data-stu-id="b60f7-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="b60f7-201">`TopologyContext` предоставляется для получения контекста топологии и особенно полезен для компонентов с поддержкой множественного параллелизма.</span><span class="sxs-lookup"><span data-stu-id="b60f7-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="b60f7-202">Пример:</span><span class="sxs-lookup"><span data-stu-id="b60f7-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="b60f7-203">Динамическая часть</span><span class="sxs-lookup"><span data-stu-id="b60f7-203">Dynamic Part</span></span>
<span data-ttu-id="b60f7-204">Следующие интерфейсы привязаны к определенным экземплярам объекта Context.</span><span class="sxs-lookup"><span data-stu-id="b60f7-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="b60f7-205">Экземпляр объекта Context создается платформой SCP.NET и передается в код пользователя.</span><span class="sxs-lookup"><span data-stu-id="b60f7-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="b60f7-206">Для нетранзакционных "воронок" с поддержкой функции подтверждения обработки данных предусмотрен следующий метод:</span><span class="sxs-lookup"><span data-stu-id="b60f7-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="b60f7-207">Для нетранзакционных "сит" с поддержкой функции подтверждения получения данных после принятия кортежа возможны только две команды: `Ack()` и `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="b60f7-208">При отправке нового кортежа данных "сита" также должны указывать привязки для него.</span><span class="sxs-lookup"><span data-stu-id="b60f7-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="b60f7-209">Существуют следующие методы.</span><span class="sxs-lookup"><span data-stu-id="b60f7-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="b60f7-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="b60f7-210">StateStore</span></span>
<span data-ttu-id="b60f7-211">`StateStore` предоставляет службы метаданных, создание монотонных последовательностей и координацию без ожидания.</span><span class="sxs-lookup"><span data-stu-id="b60f7-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="b60f7-212">Распределенные многозадачные абстракции высокого уровня могут создаваться на базе `StateStore`, включая создание распределенных блокировок, распределенных очередей, барьеров и служб транзакций.</span><span class="sxs-lookup"><span data-stu-id="b60f7-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="b60f7-213">Приложения SCP могут использовать объект `State` для сохранения определенной информации в ZooKeeper, особенно в транзакционной топологии.</span><span class="sxs-lookup"><span data-stu-id="b60f7-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="b60f7-214">Если во время этого процесса в транзакционной "воронке" происходит сбой и перезагрузка, вся необходимая информация может быть получена из ZooKeeper, и конвейер данных будет восстановлен.</span><span class="sxs-lookup"><span data-stu-id="b60f7-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="b60f7-215">Объект `StateStore` в основном обладает следующими методами.</span><span class="sxs-lookup"><span data-stu-id="b60f7-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
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
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="b60f7-216">Объект `State` в основном обладает следующими методами.</span><span class="sxs-lookup"><span data-stu-id="b60f7-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="b60f7-217">Для метода `Commit()` , когда значение simpleMode имеет значение true, соответствующий ZNode будет удален из ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="b60f7-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="b60f7-218">В противном случае будет удален текущий Z-узел и создан новый в COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="b60f7-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="b60f7-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="b60f7-219">SCPRuntime</span></span>
<span data-ttu-id="b60f7-220">SCPRuntime обеспечивает работу двух методов:</span><span class="sxs-lookup"><span data-stu-id="b60f7-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="b60f7-221">`Initialize()` используется для инициализации среды выполнения SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="b60f7-222">В этом методе процесс C#\# соединяется со стороной Java и получает параметры конфигурации и контекст топологии.</span><span class="sxs-lookup"><span data-stu-id="b60f7-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="b60f7-223">`LaunchPlugin()` используется для запуска цикла обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="b60f7-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="b60f7-224">В этом цикле подключаемый модуль C\# получает сообщения со стороны Java (включая кортежи данных и управляющие сигналы), а затем обрабатывает их с возможностью вызова метода интерфейса, описанного в коде пользователя.</span><span class="sxs-lookup"><span data-stu-id="b60f7-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="b60f7-225">Входной параметр для метода `LaunchPlugin()` является делегатом, который может возвращать объект, реализующий интерфейс ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="b60f7-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="b60f7-226">Для ISCPBatchBolt мы можем получить `StormTxAttempt` из `parms` и определить, имела ли место повторная попытка.</span><span class="sxs-lookup"><span data-stu-id="b60f7-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="b60f7-227">Этот процесс обычно происходит в подтверждающем "сите". Ознакомьтесь с примером `HelloWorldTx`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="b60f7-228">Как правило, дополнительный модуль SCP в такой ситуации может работать в двух режимах:</span><span class="sxs-lookup"><span data-stu-id="b60f7-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="b60f7-229">Режим локальной проверки. В этом режиме подключаемые модули SCP (с кодом пользователя на языке C\#) активны в Visual Studio во время фазы разработки.</span><span class="sxs-lookup"><span data-stu-id="b60f7-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="b60f7-230">В этом режиме можно использовать параметр `LocalContext`, который указывает метод для сериализации отправленных кортежей в локальные файлы и выполняет обратное считывание в память.</span><span class="sxs-lookup"><span data-stu-id="b60f7-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="b60f7-231">Обычный режим. В этом режиме подключаемые модули SCP запускаются процессом Java Storm.</span><span class="sxs-lookup"><span data-stu-id="b60f7-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="b60f7-232">Ниже дан пример запуска дополнительного модуля SCP:</span><span class="sxs-lookup"><span data-stu-id="b60f7-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="b60f7-233">Язык спецификации топологии</span><span class="sxs-lookup"><span data-stu-id="b60f7-233">Topology Specification Language</span></span>
<span data-ttu-id="b60f7-234">Спецификация топологии SCP представляет собой специализированный язык для описания и настройки топологий SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="b60f7-235">Он основан на Clojure DSL для Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) и расширен с помощью SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="b60f7-236">Спецификации топологии можно отправить напрямую в кластер Storm для выполнения через команду ***runspec***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="b60f7-237">SCP.NET добавляет следующие функции для определения транзакционной топологии:</span><span class="sxs-lookup"><span data-stu-id="b60f7-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="b60f7-238">**Новые функции**</span><span class="sxs-lookup"><span data-stu-id="b60f7-238">**New Functions**</span></span> | <span data-ttu-id="b60f7-239">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="b60f7-239">**Parameters**</span></span> | <span data-ttu-id="b60f7-240">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b60f7-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b60f7-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="b60f7-241">**tx-topolopy**</span></span> |<span data-ttu-id="b60f7-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-242">topology-name</span></span><br /><span data-ttu-id="b60f7-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="b60f7-243">spout-map</span></span><br /><span data-ttu-id="b60f7-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="b60f7-244">bolt-map</span></span> |<span data-ttu-id="b60f7-245">Определение транзакционной топологии по имени, &nbsp;карта для определения воронки и сита.</span><span class="sxs-lookup"><span data-stu-id="b60f7-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="b60f7-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="b60f7-246">**scp-tx-spout**</span></span> |<span data-ttu-id="b60f7-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-247">exec-name</span></span><br /><span data-ttu-id="b60f7-248">args</span><span class="sxs-lookup"><span data-stu-id="b60f7-248">args</span></span><br /><span data-ttu-id="b60f7-249">fields</span><span class="sxs-lookup"><span data-stu-id="b60f7-249">fields</span></span> |<span data-ttu-id="b60f7-250">Определение транзакционной "воронки".</span><span class="sxs-lookup"><span data-stu-id="b60f7-250">Define a transactional spout.</span></span> <span data-ttu-id="b60f7-251">Запускает приложение с именем ***exec-name*** и аргументами ***args***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b60f7-252">***fields*** — это поля вывода для воронки.</span><span class="sxs-lookup"><span data-stu-id="b60f7-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="b60f7-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="b60f7-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="b60f7-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-254">exec-name</span></span><br /><span data-ttu-id="b60f7-255">args</span><span class="sxs-lookup"><span data-stu-id="b60f7-255">args</span></span><br /><span data-ttu-id="b60f7-256">fields</span><span class="sxs-lookup"><span data-stu-id="b60f7-256">fields</span></span> |<span data-ttu-id="b60f7-257">Определение транзакционного пакетного "сита".</span><span class="sxs-lookup"><span data-stu-id="b60f7-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="b60f7-258">Запускает приложение с именем ***exec-name*** и аргументами ***args***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="b60f7-259">fields — это поля вывода для "воронки".</span><span class="sxs-lookup"><span data-stu-id="b60f7-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="b60f7-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="b60f7-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="b60f7-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-261">exec-name</span></span><br /><span data-ttu-id="b60f7-262">args</span><span class="sxs-lookup"><span data-stu-id="b60f7-262">args</span></span><br /><span data-ttu-id="b60f7-263">fields</span><span class="sxs-lookup"><span data-stu-id="b60f7-263">fields</span></span> |<span data-ttu-id="b60f7-264">Определение транзакционного подтверждающего "сита"</span><span class="sxs-lookup"><span data-stu-id="b60f7-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="b60f7-265">Запускает приложение с именем ***exec-name*** и аргументами ***args***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b60f7-266">***fields*** — это поля вывода для сита.</span><span class="sxs-lookup"><span data-stu-id="b60f7-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="b60f7-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="b60f7-267">**nontx-topolopy**</span></span> |<span data-ttu-id="b60f7-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-268">topology-name</span></span><br /><span data-ttu-id="b60f7-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="b60f7-269">spout-map</span></span><br /><span data-ttu-id="b60f7-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="b60f7-270">bolt-map</span></span> |<span data-ttu-id="b60f7-271">Определение нетранзакционной топологии по имени, &nbsp;карта для определения воронки и сита.</span><span class="sxs-lookup"><span data-stu-id="b60f7-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="b60f7-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="b60f7-272">**scp-spout**</span></span> |<span data-ttu-id="b60f7-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-273">exec-name</span></span><br /><span data-ttu-id="b60f7-274">args</span><span class="sxs-lookup"><span data-stu-id="b60f7-274">args</span></span><br /><span data-ttu-id="b60f7-275">fields</span><span class="sxs-lookup"><span data-stu-id="b60f7-275">fields</span></span><br /><span data-ttu-id="b60f7-276">parameters</span><span class="sxs-lookup"><span data-stu-id="b60f7-276">parameters</span></span> |<span data-ttu-id="b60f7-277">Определение нетранзакционной "воронки".</span><span class="sxs-lookup"><span data-stu-id="b60f7-277">Define a nontransactional spout.</span></span> <span data-ttu-id="b60f7-278">Запускает приложение с именем ***exec-name*** и аргументами ***args***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b60f7-279">***fields*** — это поля вывода для воронки.</span><span class="sxs-lookup"><span data-stu-id="b60f7-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="b60f7-280">Параметр ***parameters*** необязательный и используется для указания некоторых параметров, например nontransactional.ack.enabled.</span><span class="sxs-lookup"><span data-stu-id="b60f7-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="b60f7-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="b60f7-281">**scp-bolt**</span></span> |<span data-ttu-id="b60f7-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="b60f7-282">exec-name</span></span><br /><span data-ttu-id="b60f7-283">args</span><span class="sxs-lookup"><span data-stu-id="b60f7-283">args</span></span><br /><span data-ttu-id="b60f7-284">fields</span><span class="sxs-lookup"><span data-stu-id="b60f7-284">fields</span></span><br /><span data-ttu-id="b60f7-285">parameters</span><span class="sxs-lookup"><span data-stu-id="b60f7-285">parameters</span></span> |<span data-ttu-id="b60f7-286">Определение нетранзакционного "сита".</span><span class="sxs-lookup"><span data-stu-id="b60f7-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="b60f7-287">Запускает приложение с именем ***exec-name*** и аргументами ***args***.</span><span class="sxs-lookup"><span data-stu-id="b60f7-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="b60f7-288">***fields*** — это поля вывода для сита.</span><span class="sxs-lookup"><span data-stu-id="b60f7-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="b60f7-289">Параметр ***parameters*** необязательный и используется для указания некоторых параметров, например nontransactional.ack.enabled.</span><span class="sxs-lookup"><span data-stu-id="b60f7-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="b60f7-290">Для SCP.NET определены следующие ключевые слова:</span><span class="sxs-lookup"><span data-stu-id="b60f7-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="b60f7-291">**Ключевые слова**</span><span class="sxs-lookup"><span data-stu-id="b60f7-291">**Key Words**</span></span> | <span data-ttu-id="b60f7-292">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b60f7-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b60f7-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="b60f7-293">**:name**</span></span> |<span data-ttu-id="b60f7-294">Определение имени топологии</span><span class="sxs-lookup"><span data-stu-id="b60f7-294">Define the Topology Name</span></span> |
| <span data-ttu-id="b60f7-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="b60f7-295">**:topology**</span></span> |<span data-ttu-id="b60f7-296">Определение топологии с использованием функций, описанных выше, а также встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="b60f7-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="b60f7-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="b60f7-297">**:p**</span></span> |<span data-ttu-id="b60f7-298">Определение подсказок по параллелизму для каждой из "воронок" и "сита".</span><span class="sxs-lookup"><span data-stu-id="b60f7-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="b60f7-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="b60f7-299">**:config**</span></span> |<span data-ttu-id="b60f7-300">Определение параметров конфигурации или обновление существующих параметров.</span><span class="sxs-lookup"><span data-stu-id="b60f7-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="b60f7-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="b60f7-301">**:schema**</span></span> |<span data-ttu-id="b60f7-302">Определение Схемы потока данных</span><span class="sxs-lookup"><span data-stu-id="b60f7-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="b60f7-303">И часто используемые параметры:</span><span class="sxs-lookup"><span data-stu-id="b60f7-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="b60f7-304">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="b60f7-304">**Parameter**</span></span> | <span data-ttu-id="b60f7-305">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b60f7-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b60f7-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="b60f7-306">**"plugin.name"**</span></span> |<span data-ttu-id="b60f7-307">Имя exe-файла для дополнительного модуля на C#</span><span class="sxs-lookup"><span data-stu-id="b60f7-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="b60f7-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="b60f7-308">**"plugin.args"**</span></span> |<span data-ttu-id="b60f7-309">Аргументы параметров дополнительного модуля</span><span class="sxs-lookup"><span data-stu-id="b60f7-309">plugin args</span></span> |
| <span data-ttu-id="b60f7-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="b60f7-310">**"output.schema"**</span></span> |<span data-ttu-id="b60f7-311">Схема вывода</span><span class="sxs-lookup"><span data-stu-id="b60f7-311">Output schema</span></span> |
| <span data-ttu-id="b60f7-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="b60f7-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="b60f7-313">Если подтверждение обработки для нетранзакционной топологии активно.</span><span class="sxs-lookup"><span data-stu-id="b60f7-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="b60f7-314">Команда "runspec" будет реализована вместе с пакетами BITS следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b60f7-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="b60f7-315">Параметр ***resource-dir*** необязательный. Его необходимо указывать, если нужно подключить приложение C\#. В этом каталоге будет находиться приложение, а также данные зависимостей и конфигураций.</span><span class="sxs-lookup"><span data-stu-id="b60f7-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="b60f7-316">Параметр ***classpath*** также необязательный.</span><span class="sxs-lookup"><span data-stu-id="b60f7-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="b60f7-317">Он используется для указания пути к классу Java, если файл со спецификацией содержит "воронку" или "сито" на Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="b60f7-318">Прочие функции</span><span class="sxs-lookup"><span data-stu-id="b60f7-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="b60f7-319">Объявление схемы ввода и вывода</span><span class="sxs-lookup"><span data-stu-id="b60f7-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="b60f7-320">В процессе C\# пользователь может отправить кортеж. Платформе необходимо будет сериализовать этот кортеж в байты, передать его в часть Java, после чего Storm передаст его в места назначения.</span><span class="sxs-lookup"><span data-stu-id="b60f7-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="b60f7-321">В то же самое время в компоненте, находящемся далее по линии перемещения данных, процесс C\# получит кортеж данных со стороны Java и преобразует его в изначальный тип данных с помощью платформы. Эти действия производятся платформой в скрытом режиме.</span><span class="sxs-lookup"><span data-stu-id="b60f7-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="b60f7-322">Для поддержки процессов сериализации и десериализации код пользователя должен объявить схемы ввода и вывода.</span><span class="sxs-lookup"><span data-stu-id="b60f7-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="b60f7-323">Схема ввода и вывода потока — это словарь, ключом является значение Идентификатора потока, а значением — Тип колонки</span><span class="sxs-lookup"><span data-stu-id="b60f7-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="b60f7-324">Можно объявить, что компонент поддерживает несколько потоков.</span><span class="sxs-lookup"><span data-stu-id="b60f7-324">The component can have multi-streams declared.</span></span>

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


<span data-ttu-id="b60f7-325">В объект Context у нас будут добавлены следующие прикладные программные интерфейсы (API):</span><span class="sxs-lookup"><span data-stu-id="b60f7-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="b60f7-326">Код пользователя должен гарантировать, что отправленные кортежи данных подчиняются схеме, заданной для этого потока. В противном случае система создаст исключение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b60f7-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="b60f7-327">Поддержка многопоточности</span><span class="sxs-lookup"><span data-stu-id="b60f7-327">Multi-Stream Support</span></span>
<span data-ttu-id="b60f7-328">SCP предоставляет пользовательскому коду возможность получения и отправки данных с помощью множества различных потоков одновременно.</span><span class="sxs-lookup"><span data-stu-id="b60f7-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="b60f7-329">Эта возможность отражается в объекте Context, так как метод отправки получает оптимальный параметр идентификатора потока.</span><span class="sxs-lookup"><span data-stu-id="b60f7-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="b60f7-330">В объект SCP.NET Context были добавлены два метода.</span><span class="sxs-lookup"><span data-stu-id="b60f7-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="b60f7-331">Они используются при отправке кортежа или кортежей данных для обозначения идентификатора потока.</span><span class="sxs-lookup"><span data-stu-id="b60f7-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="b60f7-332">StreamId — это строка, которая должна одновременно соответствовать C\# и спецификации определения топологии.</span><span class="sxs-lookup"><span data-stu-id="b60f7-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="b60f7-333">Отправка в несуществующий поток приведет к созданию исключения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b60f7-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="b60f7-334">Группирование полей</span><span class="sxs-lookup"><span data-stu-id="b60f7-334">Fields Grouping</span></span>
<span data-ttu-id="b60f7-335">Встроенная в Storm функция объединения полей не работает должным образом в SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="b60f7-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="b60f7-336">На стороне прокси-сервера Java все поля представлены потоком байтов [], в то время как функция объединения полей использует для объединения хэш-код объекта в виде потока байтов[].</span><span class="sxs-lookup"><span data-stu-id="b60f7-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="b60f7-337">Хэш-код байтового объекта — это адрес этого объекта в памяти.</span><span class="sxs-lookup"><span data-stu-id="b60f7-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="b60f7-338">Поэтому функция объединения будет работать неправильно для двух байтовых [] объектов, у которых одинаковое значение, но различные адреса расположения.</span><span class="sxs-lookup"><span data-stu-id="b60f7-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="b60f7-339">Для SCP.NET добавлен улучшенный метод объединения, который для объединения объектов в группы использует байтовые значения[].</span><span class="sxs-lookup"><span data-stu-id="b60f7-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="b60f7-340">Синтаксис файла **SPEC** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b60f7-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="b60f7-341">В данном случае</span><span class="sxs-lookup"><span data-stu-id="b60f7-341">Here,</span></span>

1. <span data-ttu-id="b60f7-342">"scp-field-group" означает "адаптированный метод группирования полей с помощью SCP".</span><span class="sxs-lookup"><span data-stu-id="b60f7-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="b60f7-343">":tx" или "non-tx" означает транзакционную или нетранзакционную топологию.</span><span class="sxs-lookup"><span data-stu-id="b60f7-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="b60f7-344">Эта информация полезна для нас, поскольку начальных индекс в топологиях ":tx" и "non-tx" отличается.</span><span class="sxs-lookup"><span data-stu-id="b60f7-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="b60f7-345">[0,1] означает набор хэш-функций идентификаторов полей (начальное значение = "0").</span><span class="sxs-lookup"><span data-stu-id="b60f7-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="b60f7-346">Гибридная топология</span><span class="sxs-lookup"><span data-stu-id="b60f7-346">Hybrid topology</span></span>
<span data-ttu-id="b60f7-347">Изначально система Storm написана на языке Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-347">The native Storm is written in Java.</span></span> <span data-ttu-id="b60f7-348">На платформе SCP.NET эта система была усовершенствована, чтобы клиенты могли писать код C\# для обработки бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="b60f7-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="b60f7-349">Но мы также поддерживаем гибридные топологии, в которых воронки и сита возможны не только на C\#, но и на Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="b60f7-350">Задание "воронок" и "сит" на Java в файле спецификаций.</span><span class="sxs-lookup"><span data-stu-id="b60f7-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="b60f7-351">В файле спецификаций команды "scp-spout" и "scp-bolt" также можно использовать для указания "воронок " и "сит" на Java. Пример:</span><span class="sxs-lookup"><span data-stu-id="b60f7-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="b60f7-352">Здесь `microsoft.scp.example.HybridTopology.Generator` является именем класса "воронки" Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="b60f7-353">Указание classpath Java в команде runSpec</span><span class="sxs-lookup"><span data-stu-id="b60f7-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="b60f7-354">Если вы хотите отправить топологию с "воронками" и "ситами" Java, сначала необходимо скомпилировать "воронки" или "сита" Java и получить JAR-файлы.</span><span class="sxs-lookup"><span data-stu-id="b60f7-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="b60f7-355">Затем при отправке топологии нужно указать classpath Java, который содержит JAR-файлы.</span><span class="sxs-lookup"><span data-stu-id="b60f7-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="b60f7-356">Пример:</span><span class="sxs-lookup"><span data-stu-id="b60f7-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="b60f7-357">**examples\\HybridTopology\\java\\target\\** — папка с JAR-файлом воронки или сита Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="b60f7-358">Сериализация или десериализация между Java и C#</span><span class="sxs-lookup"><span data-stu-id="b60f7-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="b60f7-359">Компонент SCP включает в себя часть C\# и часть Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="b60f7-360">Чтобы обеспечить взаимодействия с собственными воронками и ситами, Java нужно выполнять сериализацию и десериализацию между частями Java и C\#, как показано на следующей схеме.</span><span class="sxs-lookup"><span data-stu-id="b60f7-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Схема компонента Java, отправляющего данные в компонент SCP, который отправляет данные в компонент Java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="b60f7-362">**Сериализация на стороне Java и десериализация на стороне C\#**</span><span class="sxs-lookup"><span data-stu-id="b60f7-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="b60f7-363">Для начала нужно обеспечить стандартное применение сериализации на стороне Java и десериализации на стороне C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="b60f7-364">Метод сериализации на стороне Java можно задать через файл спецификаций:</span><span class="sxs-lookup"><span data-stu-id="b60f7-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="b60f7-365">Метод десериализации на стороне C\# можно задать через программный пользовательский код C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="b60f7-366">Стандартная сериализация должна работать должным образом в большинстве случаев, если тип данных не слишком сложный.</span><span class="sxs-lookup"><span data-stu-id="b60f7-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="b60f7-367">В некоторых случаях пользователь может добавить свой тип реализации — либо из-за сложного типа данных, либо из-за того, что стандартная реализация не отвечает требованиям пользователя.</span><span class="sxs-lookup"><span data-stu-id="b60f7-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="b60f7-368">Интерфейс сериализации на стороне Java задается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b60f7-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="b60f7-369">Интерфейс сериализации на стороне C\# задается следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b60f7-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="b60f7-370">Общедоступный интерфейс ICustomizedInteropCSharpDeserializer.</span><span class="sxs-lookup"><span data-stu-id="b60f7-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="b60f7-371">**Сериализация на стороне C\# и десериализация на стороне Java**</span><span class="sxs-lookup"><span data-stu-id="b60f7-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="b60f7-372">Метод десериализации на стороне C\# следует указать в пользовательском коде C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="b60f7-373">Метод десериализации в части Java следует указать в SPEC-файле.</span><span class="sxs-lookup"><span data-stu-id="b60f7-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="b60f7-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="b60f7-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="b60f7-375">Здесь microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer — имя десериализатора, а microsoft.scp.example.HybridTopology.Person — целевой класс, в который десериализуются данные.</span><span class="sxs-lookup"><span data-stu-id="b60f7-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="b60f7-376">Пользователь может также подключить свою собственную реализацию сериализатора C\# и десериализатора Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="b60f7-377">Это интерфейс для сериализатора C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="b60f7-378">Это интерфейс для десериализатора Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="b60f7-379">Хост-режим SCP</span><span class="sxs-lookup"><span data-stu-id="b60f7-379">SCP Host Mode</span></span>
<span data-ttu-id="b60f7-380">В этом режиме пользователь может компилировать код в DLL-файл и использовать предоставляемый SCP файл SCPHost.exe, чтобы задать топологию.</span><span class="sxs-lookup"><span data-stu-id="b60f7-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="b60f7-381">Соответствующий файл спецификации выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b60f7-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="b60f7-382">Здесь в качестве `plugin.name` указан `SCPHost.exe` из пакета SDK для SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="b60f7-383">SCPHost.exe принимает только три параметра:</span><span class="sxs-lookup"><span data-stu-id="b60f7-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="b60f7-384">Первый из них — это имя библиотеки DLL. В данном примере это `"HelloWorld.dll"`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="b60f7-385">Второй — это имя класса. В данном примере это `"Scp.App.HelloWorld.Generator"`.</span><span class="sxs-lookup"><span data-stu-id="b60f7-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="b60f7-386">Третий — это общедоступный статический метод, который можно вызвать для того, чтобы получить экземпляр ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="b60f7-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="b60f7-387">В хост-режиме код пользователя компилируется в DLL-файл и вызывается платформой SCP.</span><span class="sxs-lookup"><span data-stu-id="b60f7-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="b60f7-388">Поэтому платформа SCP получает полный контроль над всей логической схемой обработки информации.</span><span class="sxs-lookup"><span data-stu-id="b60f7-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="b60f7-389">Мы рекомендуем нашим клиентам задавать топологию через хост-режим SCP, поскольку это упрощает процесс программирования, способствует увеличению его гибкости, а также лучшей совместимости с предыдущими версиями.</span><span class="sxs-lookup"><span data-stu-id="b60f7-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="b60f7-390">Примеры программирования для SCP</span><span class="sxs-lookup"><span data-stu-id="b60f7-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="b60f7-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="b60f7-391">HelloWorld</span></span>
<span data-ttu-id="b60f7-392">**HelloWorld** — это простой пример, на котором можно продемонстрировать удобство работы с SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="b60f7-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="b60f7-393">Она использует нетранзакционную топологию, в которой воронка называется **generator**, а два сита — **splitter** и **counter**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="b60f7-394">Воронка **generator** случайным образом создает предложения и отправляет их в сито **splitter**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="b60f7-395">Сито **splitter** разбивает эти предложения на слова и отправляет их в сито **counter**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="b60f7-396">"Сито" "counter" использует словарь для записи частоты употребления каждого слова.</span><span class="sxs-lookup"><span data-stu-id="b60f7-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="b60f7-397">Для этого примера существует два файла спецификации — **HelloWorld.spec** и **HelloWorld\_EnableAck.spec**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="b60f7-398">В программном коде C\# можно определить, задействована ли функция подтверждения, получив pluginConf со стороны Java.</span><span class="sxs-lookup"><span data-stu-id="b60f7-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="b60f7-399">Если служба подтверждения задействована, то в "воронке" словарь используется для помещения неподтвержденных кортежей во временную память.</span><span class="sxs-lookup"><span data-stu-id="b60f7-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="b60f7-400">Если вызывается Fail(), то кортежи данных с ошибками будут отсылаться повторно.</span><span class="sxs-lookup"><span data-stu-id="b60f7-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="b60f7-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="b60f7-401">HelloWorldTx</span></span>
<span data-ttu-id="b60f7-402">Пример **HelloWorldTx** демонстрирует, как реализовать транзакционную топологию.</span><span class="sxs-lookup"><span data-stu-id="b60f7-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="b60f7-403">В ней воронка называется **generator**, пакетные сита — **partial-count**, а подтверждающее сито — **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="b60f7-404">В примере содержатся три предварительно созданных текстовых файла: **DataSource0.txt**, **DataSource1.txt** и **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="b60f7-405">При каждой транзакции воронка **generator** случайным образом выбирает два из трех предварительно созданных файла и отправляет их имена в сито **partial-count**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="b60f7-406">Сито **partial-count** сначала получает имя файла из полученного кортежа, открывает этот файл и считает количество слов в нем, после чего отправляет полученное значение в сито **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="b60f7-407">"Сито" **count-sum** вычисляет итоговое количество.</span><span class="sxs-lookup"><span data-stu-id="b60f7-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="b60f7-408">Для достижения семантики **только однажды** подтверждающее сито **count-sum** должно определить перезапущенные транзакции.</span><span class="sxs-lookup"><span data-stu-id="b60f7-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="b60f7-409">В этом примере транзакция имеет статическую переменную-член.</span><span class="sxs-lookup"><span data-stu-id="b60f7-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="b60f7-410">После создания экземпляра ISCPBatchBolt он получает `txAttempt` из входящих параметров.</span><span class="sxs-lookup"><span data-stu-id="b60f7-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
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

<span data-ttu-id="b60f7-411">После вызова `FinishBatch()` параметр `lastCommittedTxId` обновляется, если транзакция не была перезапущена.</span><span class="sxs-lookup"><span data-stu-id="b60f7-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="b60f7-412">Гибридная топология</span><span class="sxs-lookup"><span data-stu-id="b60f7-412">HybridTopology</span></span>
<span data-ttu-id="b60f7-413">Данная топология содержит воронку на Java и сито на C\#.</span><span class="sxs-lookup"><span data-stu-id="b60f7-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="b60f7-414">В ней используются стандартные для платформы SCP процессы сериализации и десериализации.</span><span class="sxs-lookup"><span data-stu-id="b60f7-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="b60f7-415">Сведения о файле спецификаций см. в файле **HybridTopology.spec** в папке **examples\\HybridTopology**, а сведения об указании classpath Java — в файле **SubmitTopology.bat**.</span><span class="sxs-lookup"><span data-stu-id="b60f7-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="b60f7-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="b60f7-416">SCPHostDemo</span></span>
<span data-ttu-id="b60f7-417">Этот пример по своей сути не отличается от примера с программой HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="b60f7-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="b60f7-418">Единственное отличие заключается в том, что пользовательский код компилируется в DLL-файл и топология задается через файл SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b60f7-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="b60f7-419">Дополнительная информация содержится в разделе "Хост-режим SCP".</span><span class="sxs-lookup"><span data-stu-id="b60f7-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b60f7-420">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b60f7-420">Next Steps</span></span>
<span data-ttu-id="b60f7-421">Примеры топологий Storm, созданных с помощью SCP, приведены в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="b60f7-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="b60f7-422">Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b60f7-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b60f7-423">Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b60f7-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="b60f7-424">Создание нескольких потоков данных в топологии Storm на C#</span><span class="sxs-lookup"><span data-stu-id="b60f7-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="b60f7-425">Использование Power Bi для визуализации данных из топологии Storm</span><span class="sxs-lookup"><span data-stu-id="b60f7-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="b60f7-426">Обработка данных с датчиков автомобиля из концентраторов событий с использованием Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b60f7-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="b60f7-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span><span class="sxs-lookup"><span data-stu-id="b60f7-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="b60f7-428">Сопоставление событий с помощью Storm и HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b60f7-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

