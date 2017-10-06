---
title: "aaaUse Kafka Apache с Storm на HDInsight - Azure | Документы Microsoft"
description: "Платформа Apache Kafka устанавливается вместе с Apache Storm в службе HDInsight. Узнайте, как toowrite tooKafka и затем прочитать из него, используя hello KafkaBolt и KafkaSpout компоненты, предоставляемые с Storm. Также узнаете, как toouse hello toodefine framework меняется и отправить Storm топологии."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="b77f0-105">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b77f0-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="b77f0-106">Узнайте, как tooread Apache Storm toouse из и записи tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="b77f0-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="b77f0-107">Этот пример также демонстрирует, как данные toosave из toohello топологии Storm HDFS-совместимой файловой системы, используемый HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b77f0-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="b77f0-108">Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Storm на HDInsight и Kafka в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b77f0-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="b77f0-109">Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластер Storm взаимодействовать с hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="b77f0-110">После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.</span><span class="sxs-lookup"><span data-stu-id="b77f0-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="b77f0-111">Получение кода hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-111">Get hello code</span></span>

<span data-ttu-id="b77f0-112">Hello код для примера hello, используемые в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="b77f0-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="b77f0-113">toocompile этого проекта требуется следующая конфигурация для среды разработки hello:</span><span class="sxs-lookup"><span data-stu-id="b77f0-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="b77f0-114">Пакет [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="b77f0-115">Для HDInsight 3.5 или более поздней версии требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="b77f0-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="b77f0-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="b77f0-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="b77f0-117">Такой клиент SSH (требуется hello `ssh` и `scp` команд) — сведения в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b77f0-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="b77f0-118">Текстовый редактор или интегрированная среда разработки.</span><span class="sxs-lookup"><span data-stu-id="b77f0-118">A text editor or IDE.</span></span>

<span data-ttu-id="b77f0-119">Hello следующие переменные среды можно задать при установке Java и hello JDK на рабочей станции разработки.</span><span class="sxs-lookup"><span data-stu-id="b77f0-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="b77f0-120">Тем не менее необходимо проверить, они существуют, и что они содержат правильные значения hello для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="b77f0-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="b77f0-121">`JAVA_HOME`-должен указывать toohello каталог, где hello JDK установлен.</span><span class="sxs-lookup"><span data-stu-id="b77f0-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="b77f0-122">`PATH`-должен содержать hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="b77f0-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="b77f0-123">`JAVA_HOME`(или эквивалентный путь hello).</span><span class="sxs-lookup"><span data-stu-id="b77f0-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b77f0-124">`JAVA_HOME\bin`(или эквивалентный путь hello).</span><span class="sxs-lookup"><span data-stu-id="b77f0-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b77f0-125">Hello каталоге установки Maven.</span><span class="sxs-lookup"><span data-stu-id="b77f0-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="b77f0-126">Создавать кластеры hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-126">Create hello clusters</span></span>

<span data-ttu-id="b77f0-127">Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="b77f0-128">Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="b77f0-129">В этом примере hello Kafka и Storm кластеры расположены в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="b77f0-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="b77f0-130">Hello следующей схеме показаны связи потоки между кластерами hello:</span><span class="sxs-lookup"><span data-stu-id="b77f0-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Схема кластеров Storm и Kafka в виртуальной сети Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="b77f0-132">Другие службы в кластере hello такие, как можно получить через SSH и Ambari hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="b77f0-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="b77f0-133">Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="b77f0-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="b77f0-134">Можно создать виртуальную сеть Azure, Kafka, и Storm кластеры вручную, но это проще toouse шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b77f0-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="b77f0-135">Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Storm кластеры tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b77f0-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="b77f0-136">Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b77f0-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="b77f0-137">Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="b77f0-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="b77f0-138">Создает hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="b77f0-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="b77f0-139">Группа ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b77f0-139">Azure resource group</span></span>
    * <span data-ttu-id="b77f0-140">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="b77f0-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="b77f0-141">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="b77f0-141">Azure Storage account</span></span>
    * <span data-ttu-id="b77f0-142">Kafka в HDInsight версии 3.6 (три рабочих узла)</span><span class="sxs-lookup"><span data-stu-id="b77f0-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="b77f0-143">Storm в HDInsight версии 3.6 (три рабочих узла)</span><span class="sxs-lookup"><span data-stu-id="b77f0-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="b77f0-144">доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="b77f0-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="b77f0-145">Этот шаблон создает кластер Kafka, содержащий три рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="b77f0-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="b77f0-146">Hello используйте следующие рекомендации toopopulate hello записей на hello **развертывания пользовательского** колонки:</span><span class="sxs-lookup"><span data-stu-id="b77f0-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="b77f0-148">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="b77f0-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="b77f0-149">Эта группа содержит кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="b77f0-150">**Расположение**: выберите расположение территориально закрыть tooyou.</span><span class="sxs-lookup"><span data-stu-id="b77f0-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="b77f0-151">**Базовые имена кластеров**: это значение используется как базовое имя hello для кластеров Storm и Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="b77f0-152">Например, если ввести **hdi**, будет создан кластер Storm **storm-hdi** и кластер Kafka **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="b77f0-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="b77f0-153">**Имя входа пользователя кластера**: hello имя пользователя администратора для hello Storm и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="b77f0-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="b77f0-154">**Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Storm и Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b77f0-155">**Имя пользователя SSH**: hello toocreate пользователя SSH для hello Storm и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="b77f0-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b77f0-156">**Пароль SSH**: hello пароль пользователя SSH hello для hello Storm и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="b77f0-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="b77f0-157">Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.</span><span class="sxs-lookup"><span data-stu-id="b77f0-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="b77f0-158">Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**.</span><span class="sxs-lookup"><span data-stu-id="b77f0-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="b77f0-159">Занимает около 20 минут toocreate hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="b77f0-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="b77f0-160">После создания ресурсов hello отображается колонке hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b77f0-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="b77f0-162">Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ storm** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="b77f0-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="b77f0-163">Использовать эти имена на последующих этапах при подключении toohello кластеров.</span><span class="sxs-lookup"><span data-stu-id="b77f0-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="b77f0-164">Общие сведения о коде hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-164">Understanding hello code</span></span>

<span data-ttu-id="b77f0-165">Этот проект содержит две топологии:</span><span class="sxs-lookup"><span data-stu-id="b77f0-165">This project contains two topologies:</span></span>

* <span data-ttu-id="b77f0-166">**KafkaWriter**: определяется hello **writer.yaml** файл, в этой топологии записывает tooKafka случайных предложений, с помощью hello в состав Apache Storm KafkaBolt.</span><span class="sxs-lookup"><span data-stu-id="b77f0-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="b77f0-167">Данная топология использует пользовательский **SentenceSpout** предложений случайных toogenerate компонента.</span><span class="sxs-lookup"><span data-stu-id="b77f0-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="b77f0-168">**KafkaReader**: определяется hello **reader.yaml** файла, в этой топологии считывает данные из Kafka с помощью hello в состав Apache Storm KafkaSpout, то журналы hello toostdout данных.</span><span class="sxs-lookup"><span data-stu-id="b77f0-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="b77f0-169">В этой топологии использует hello Storm HdfsBolt toowrite данные toodefault хранилища для кластера Storm hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="b77f0-170">Flux</span><span class="sxs-lookup"><span data-stu-id="b77f0-170">Flux</span></span>

<span data-ttu-id="b77f0-171">топологии Hello определяются с помощью [меняется](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b77f0-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="b77f0-172">Поток был введен в Storm 0.10.x, а также конфигурация топологии hello tooseparate из кода hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="b77f0-173">Для топологий, которые используют framework определен hello hello топологии определяется в файле YAML.</span><span class="sxs-lookup"><span data-stu-id="b77f0-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="b77f0-174">Hello YAML файл может быть частью hello топологии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="b77f0-175">Он также может быть автономный файл, используемый при отправке hello топологии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="b77f0-176">Flux также поддерживает подстановку переменных во время выполнения, которая используется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="b77f0-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="b77f0-177">Hello следующие параметры устанавливаются во время выполнения для следующих топологий:</span><span class="sxs-lookup"><span data-stu-id="b77f0-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="b77f0-178">`${kafka.topic}`: имя hello hello Kafka раздел, в котором топологии hello чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="b77f0-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="b77f0-179">`${kafka.broker.hosts}`: hello размещается, отслеживающим Kafka hello и запустить на.</span><span class="sxs-lookup"><span data-stu-id="b77f0-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="b77f0-180">При написании tooKafka сведения broker Hello используется hello KafkaBolt.</span><span class="sxs-lookup"><span data-stu-id="b77f0-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="b77f0-181">`${kafka.zookeeper.hosts}`: hello узлов, выполняющееся в Zookeeper hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="b77f0-182">Дополнительные сведения о топологиях Flux см. на странице [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b77f0-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="b77f0-183">Загрузите и скомпилируйте проект hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-183">Download and compile hello project</span></span>

1. <span data-ttu-id="b77f0-184">В среде разработки загрузите проект hello из [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), откройте командную строку и измените расположение toohello каталоги, загруженный проект hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="b77f0-185">Из hello **hdinsight storm-java kafka** каталога, используйте hello следующую команду toocompile hello проекта и создайте пакет для развертывания:</span><span class="sxs-lookup"><span data-stu-id="b77f0-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="b77f0-186">процесс Hello пакета создается файл с именем `KafkaTopology-1.0-SNAPSHOT.jar` в hello `target` каталога.</span><span class="sxs-lookup"><span data-stu-id="b77f0-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="b77f0-187">Используйте следующие команды toocopy hello пакета tooyour Storm в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="b77f0-188">Замените **USERNAME** с именем пользователя hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b77f0-189">Замените **базовым ИМЕНЕМ** с базовым именем hello использовалась при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="b77f0-190">При появлении запроса введите пароль hello, используемый при создании кластеров hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="b77f0-191">Настройка топологии hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-191">Configure hello topology</span></span>

1. <span data-ttu-id="b77f0-192">Используйте один из следующих методов toodiscover hello hello Kafka broker узлов:</span><span class="sxs-lookup"><span data-stu-id="b77f0-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b77f0-193">Hello Bash предполагается, что `$CLUSTERNAME` содержит hello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b77f0-194">Также предполагается, что [jq](https://stedolan.github.io/jq/) установлен.</span><span class="sxs-lookup"><span data-stu-id="b77f0-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b77f0-195">При появлении запроса введите hello пароль для учетной записи входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b77f0-196">Hello возвращаемое значение аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="b77f0-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="b77f0-197">Хотя может быть более двух узлов брокера для кластера, не обязательно tooprovide полный список всех узлов tooclients.</span><span class="sxs-lookup"><span data-stu-id="b77f0-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b77f0-198">Достаточно указать один или два.</span><span class="sxs-lookup"><span data-stu-id="b77f0-198">One or two is enough.</span></span>

2. <span data-ttu-id="b77f0-199">Используйте один из hello следующие методы toodiscover hello Kafka Zookeeper узлов.</span><span class="sxs-lookup"><span data-stu-id="b77f0-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b77f0-200">Hello Bash предполагается, что `$CLUSTERNAME` содержит hello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b77f0-201">Также предполагается, что [jq](https://stedolan.github.io/jq/) установлен.</span><span class="sxs-lookup"><span data-stu-id="b77f0-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b77f0-202">При появлении запроса введите hello пароль для учетной записи входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b77f0-203">Hello возвращаемое значение аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="b77f0-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="b77f0-204">При наличии более двух узлов Zookeeper, tooprovide полный список всех узлов tooclients не обязательно.</span><span class="sxs-lookup"><span data-stu-id="b77f0-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b77f0-205">Достаточно указать один или два.</span><span class="sxs-lookup"><span data-stu-id="b77f0-205">One or two is enough.</span></span>

    <span data-ttu-id="b77f0-206">Сохраните это значение, так как оно будет использовано позже.</span><span class="sxs-lookup"><span data-stu-id="b77f0-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="b77f0-207">Изменить hello `dev.properties` файл в корневой hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b77f0-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="b77f0-208">Добавьте hello брокера и Zookeeper узлов сведения toohello совпадающие строки в этом файле.</span><span class="sxs-lookup"><span data-stu-id="b77f0-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="b77f0-209">Hello в примере настраивается с помощью значений образец hello hello предыдущих шагах:</span><span class="sxs-lookup"><span data-stu-id="b77f0-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="b77f0-210">Сохранить hello `dev.properties` файл и затем с помощью hello следующие команды tooupload его toohello Storm кластера:</span><span class="sxs-lookup"><span data-stu-id="b77f0-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="b77f0-211">Замените **USERNAME** с именем пользователя hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b77f0-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b77f0-212">Замените **базовым ИМЕНЕМ** с базовым именем hello использовалась при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="b77f0-213">Запуск модуля записи hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-213">Start hello writer</span></span>

1. <span data-ttu-id="b77f0-214">Используйте следующие tooconnect toohello Storm кластера с помощью SSH hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="b77f0-215">Замените **USERNAME** с именем пользователя hello SSH, используемые при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="b77f0-216">Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="b77f0-217">При появлении запроса введите пароль hello, используемый при создании кластеров hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="b77f0-218">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b77f0-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b77f0-219">В hello SSH-подключения используйте hello, следующая команда toocreate hello Kafka раздел, используемый hello топологии:</span><span class="sxs-lookup"><span data-stu-id="b77f0-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="b77f0-220">Замените `$KAFKAZKHOSTS` с hello Zookeeper размещения информации, полученной в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="b77f0-221">В кластер Storm toohello подключения SSH hello используйте следующие команды toostart hello записи топологии hello:</span><span class="sxs-lookup"><span data-stu-id="b77f0-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="b77f0-222">используются следующие параметры Hello, используемые с данной командой.</span><span class="sxs-lookup"><span data-stu-id="b77f0-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="b77f0-223">`org.apache.storm.flux.Flux`: Используется tooconfigure меняется и выполнение в этой топологии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="b77f0-224">`--remote`: Отправьте tooNimbus топологии hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="b77f0-225">Топология Hello распределяется по hello рабочих узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="b77f0-226">`-R /writer.yaml`: Использование hello `writer.yaml` файл tooconfigure hello топологии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="b77f0-227">`-R`Указывает, что этот ресурс включен в hello jar-файл.</span><span class="sxs-lookup"><span data-stu-id="b77f0-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="b77f0-228">Он находится в корне hello hello jar, поэтому `/writer.yaml` — tooit путь hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="b77f0-229">`--filter`: Заполнения записей в hello `writer.yaml` топологии с использованием значений в hello `dev.properties` файла.</span><span class="sxs-lookup"><span data-stu-id="b77f0-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="b77f0-230">Например, hello значение hello `kafka.topic` запись в файле hello — используется tooreplace hello `${kafka.topic}` запись в определении топологии hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="b77f0-231">После запуска hello топологии, используйте hello следующая команда tooverify, записывает данные toohello Kafka раздела:</span><span class="sxs-lookup"><span data-stu-id="b77f0-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="b77f0-232">Замените `$KAFKAZKHOSTS` с hello Zookeeper размещения информации, полученной в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="b77f0-233">Эта команда использует сценарий, поставляемых с Kafka toomonitor hello раздела.</span><span class="sxs-lookup"><span data-stu-id="b77f0-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="b77f0-234">Через некоторое время он запущен возвращение случайных предложения, которые были записаны toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="b77f0-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="b77f0-235">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="b77f0-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="b77f0-236">Используйте сочетание клавиш Ctrl + c toostop hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="b77f0-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="b77f0-237">Запустите средство чтения hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-237">Start hello reader</span></span>

1. <span data-ttu-id="b77f0-238">В кластер Storm toohello сеанс SSH hello используйте следующие команды toostart hello чтения топологии hello:</span><span class="sxs-lookup"><span data-stu-id="b77f0-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="b77f0-239">После запуска топологии hello, откройте hello Storm пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b77f0-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="b77f0-240">Этот веб-интерфейс расположен по адресу https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="b77f0-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="b77f0-241">Замените __базовым ИМЕНЕМ__ с базовым именем hello использовалась при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="b77f0-242">При появлении запроса, используйте имя входа администратора hello (по умолчанию, `admin`) и пароль, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="b77f0-243">Можно увидеть примерно toohello веб-страницы, следующие изображения:</span><span class="sxs-lookup"><span data-stu-id="b77f0-243">You see a web page similar toohello following image:</span></span>

    ![Пользовательский интерфейс Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="b77f0-245">Hello Storm пользовательского интерфейса, выберите hello __kafka чтения__ ссылку в hello __топологии Сводка__ статьи toodisplay сведения о hello __kafka чтения__ топологии.</span><span class="sxs-lookup"><span data-stu-id="b77f0-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Топология Аннотация hello Storm пользовательского веб-интерфейса](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="b77f0-247">toodisplay сведения об экземплярах hello компонента средства ведения журнала молнии hello, выберите hello __молнии средства ведения журнала__ ссылку в hello __винты (все время)__ раздела.</span><span class="sxs-lookup"><span data-stu-id="b77f0-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Средства ведения журнала молнии ссылку в разделе винты hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="b77f0-249">В hello __исполнителей__ выберите ссылку в hello __порт__ столбца toodisplay запись сведений об этом экземпляре компонента hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Ссылка Executors](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="b77f0-251">Hello журнала содержит журнал hello чтение данных из раздела Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b77f0-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="b77f0-252">Hello сведения в журнале hello — примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="b77f0-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="b77f0-253">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="b77f0-253">Stop hello topologies</span></span>

<span data-ttu-id="b77f0-254">Из кластера Storm toohello сеансу SSH используйте следующие команды toostop hello Storm топологии hello:</span><span class="sxs-lookup"><span data-stu-id="b77f0-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="b77f0-255">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="b77f0-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b77f0-256">С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b77f0-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="b77f0-257">Удаление группы ресурсов hello удаляет все ресурсы, созданные после этого документа.</span><span class="sxs-lookup"><span data-stu-id="b77f0-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b77f0-258">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b77f0-258">Next steps</span></span>

<span data-ttu-id="b77f0-259">Дополнительные примеры топологий, которые можно использовать со Storm в HDInsight, см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b77f0-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="b77f0-260">Сведения о развертывании и мониторинге топологий в HDInsight под управлением Linux см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b77f0-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>