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
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="1d5f8-105">Пример потоковой передачи Apache Spark (DStream) с использованием Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d5f8-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="1d5f8-106">Узнайте, как toouse данных toostream Spark Apache Spark в или из Kafka Apache на HDInsight с помощью DStreams.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="1d5f8-107">В этом примере используется записной книжке Jupyter, который выполняется на кластере Spark hello.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="1d5f8-108">Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Spark в HDInsight и Kafka в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="1d5f8-109">Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластера Spark взаимодействовать с hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="1d5f8-110">После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="1d5f8-111">Создавать кластеры hello</span><span class="sxs-lookup"><span data-stu-id="1d5f8-111">Create hello clusters</span></span>

<span data-ttu-id="1d5f8-112">Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="1d5f8-113">Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="1d5f8-114">В этом примере hello Kafka и Spark кластеры расположены в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="1d5f8-115">Hello следующей схеме показаны связи потоки между кластерами hello:</span><span class="sxs-lookup"><span data-stu-id="1d5f8-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="1d5f8-117">То, что Kafka себя ограниченный toocommunication в виртуальной сети hello, другие службы в кластере hello такие, как можно получить через SSH и Ambari hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="1d5f8-118">Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="1d5f8-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="1d5f8-119">Вы можете создать виртуальную сеть Azure, Kafka и Spark кластеров вручную, это упрощает toouse шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="1d5f8-120">Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Spark кластеры tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="1d5f8-121">Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="1d5f8-122">Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1d5f8-123">доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="1d5f8-124">Этот шаблон создает кластер Kafka, содержащий три рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="1d5f8-125">Этот шаблон создает кластер HDInsight 3.6 для Kafka и Spark.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="1d5f8-126">После записи hello toopopulate сведений на hello hello используйте **развертывания пользовательского** колонки:</span><span class="sxs-lookup"><span data-stu-id="1d5f8-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="1d5f8-128">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="1d5f8-129">Эта группа содержит кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="1d5f8-130">**Расположение**: выберите расположение территориально закрыть tooyou.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="1d5f8-131">**Базовые имена кластеров**: это значение используется как базовое имя hello для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="1d5f8-132">Например, если ввести **hdi**, будет создан кластер Spark с именем spark-hdi__ и кластер Kafka с именем **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="1d5f8-133">**Имя входа пользователя кластера**: hello имя пользователя администратора для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1d5f8-134">**Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Spark и Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1d5f8-135">**Имя пользователя SSH**: hello toocreate пользователя SSH для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1d5f8-136">**Пароль SSH**: hello пароль пользователя SSH hello для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="1d5f8-137">Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="1d5f8-138">Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="1d5f8-139">Занимает около 20 минут toocreate hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="1d5f8-140">После создания ресурсов hello предпринимается колонке перенаправленный tooa hello группы ресурсов, содержащий кластеров hello и панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="1d5f8-142">Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ spark** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="1d5f8-143">Использовать эти имена на последующих этапах при подключении toohello кластеров.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="1d5f8-144">С помощью ноутбуков hello</span><span class="sxs-lookup"><span data-stu-id="1d5f8-144">Use hello notebooks</span></span>

<span data-ttu-id="1d5f8-145">Hello код для примера hello, описанные в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="1d5f8-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="1d5f8-146">Следуйте указаниям hello hello `README.md` файл toocomplete в этом примере.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="1d5f8-147">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="1d5f8-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1d5f8-148">С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="1d5f8-149">Удаление группы hello удаляет все ресурсы, созданные после этого документа, hello виртуальной сети Azure и учетной записи хранения, используемые в кластерах hello.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d5f8-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d5f8-150">Next steps</span></span>

<span data-ttu-id="1d5f8-151">В этом примере вы узнали, как toouse усилить tooread и записи tooKafka.</span><span class="sxs-lookup"><span data-stu-id="1d5f8-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="1d5f8-152">Используйте следующие ссылки toodiscover hello других способов toowork с Kafka:</span><span class="sxs-lookup"><span data-stu-id="1d5f8-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="1d5f8-153">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="1d5f8-153">[Get started with Apache Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="1d5f8-154">Используйте MirrorMaker toocreate реплику Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d5f8-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="1d5f8-155">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d5f8-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

