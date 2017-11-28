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
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="5ec86-104">Использование структурированной потоковой передачи Spark с Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ec86-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="5ec86-105">Узнайте, как toouse Spark структурированных потоковой передачи данных tooread из Kafka Apache на Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ec86-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="5ec86-106">Структурированная потоковая передача Spark — это механизм обработки потока, встроенный в Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="5ec86-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="5ec86-107">Он позволяет вам вычисления потоковой передачи tooexpress hello то же, что вычисление пакета со статическими данными.</span><span class="sxs-lookup"><span data-stu-id="5ec86-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="5ec86-108">Дополнительные сведения о структурированной потоковой передачи. в разделе hello [структурированных потоковой передачи руководство по программированию [альфа]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) с программами.</span><span class="sxs-lookup"><span data-stu-id="5ec86-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ec86-109">В этом примере используется Spark 2.1 в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="5ec86-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="5ec86-110">Структурированная потоковая передача рассматривается как __альфа-версия__ в Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="5ec86-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="5ec86-111">Hello в данном пошаговом руководстве создайте другой группы ресурсов Azure, которая содержит как Spark в HDInsight и Kafka в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ec86-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="5ec86-112">Эти кластеры, что оба, расположенного внутри виртуальной сети Azure, что позволяет hello toodirectly кластера Spark взаимодействовать с hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="5ec86-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="5ec86-113">После завершения шагов hello в этом документе помните toodelete hello кластеров tooavoid лишних расходов.</span><span class="sxs-lookup"><span data-stu-id="5ec86-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="5ec86-114">Создавать кластеры hello</span><span class="sxs-lookup"><span data-stu-id="5ec86-114">Create hello clusters</span></span>

<span data-ttu-id="5ec86-115">Kafka Apache на HDInsight не предоставляет доступа toohello Kafka брокеры через общедоступный Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="5ec86-116">Все, что Здравствуйте, обсуждения tooKafka должен находиться в одной виртуальной сети Azure hello в виде узлов hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="5ec86-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="5ec86-117">В этом примере hello Kafka и Spark кластеры расположены в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="5ec86-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="5ec86-118">Hello следующей схеме показаны связи потоки между кластерами hello:</span><span class="sxs-lookup"><span data-stu-id="5ec86-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="5ec86-120">Hello Kafka службы — ограниченный toocommunication в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="5ec86-121">Другие службы в кластере hello, такие как SSH и Ambari, могут быть доступны через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="5ec86-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="5ec86-122">Дополнительные сведения о hello открытых портов, доступных с HDInsight см. в разделе [порты и URI, используемый HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="5ec86-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="5ec86-123">Вы можете создать виртуальную сеть Azure, Kafka и Spark кластеров вручную, это упрощает toouse шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5ec86-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="5ec86-124">Используйте hello следующие шаги toodeploy виртуальной сети Azure, Kafka, и Spark кластеры tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5ec86-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="5ec86-125">Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ec86-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="5ec86-126">Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="5ec86-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="5ec86-127">Этот шаблон создает hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="5ec86-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="5ec86-128">Kafka в кластере HDInsight 3.5;</span><span class="sxs-lookup"><span data-stu-id="5ec86-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="5ec86-129">Spark в кластере HDInsight 3.6;</span><span class="sxs-lookup"><span data-stu-id="5ec86-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="5ec86-130">Виртуальная сеть Azure, содержащий hello кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ec86-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5ec86-131">Hello структурированных потоковой передачи записной книжки используются в этом примере требуется Spark в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="5ec86-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="5ec86-132">При использовании более ранней версии Spark на HDInsight, возникнут ошибки при использовании записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="5ec86-133">После записи hello toopopulate сведений на hello hello используйте **развертывания пользовательского** колонки:</span><span class="sxs-lookup"><span data-stu-id="5ec86-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="5ec86-135">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="5ec86-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="5ec86-136">Эта группа содержит кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="5ec86-137">**Расположение**: выберите расположение территориально закрыть tooyou.</span><span class="sxs-lookup"><span data-stu-id="5ec86-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="5ec86-138">**Базовые имена кластеров**: это значение используется как базовое имя hello для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="5ec86-139">Например, если ввести **hdi**, будет создан кластер Spark с именем spark-hdi__ и кластер Kafka с именем **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="5ec86-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="5ec86-140">**Имя входа пользователя кластера**: hello имя пользователя администратора для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5ec86-141">**Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Spark и Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5ec86-142">**Имя пользователя SSH**: hello toocreate пользователя SSH для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5ec86-143">**Пароль SSH**: hello пароль пользователя SSH hello для hello Spark и Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="5ec86-144">Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.</span><span class="sxs-lookup"><span data-stu-id="5ec86-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="5ec86-145">Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**.</span><span class="sxs-lookup"><span data-stu-id="5ec86-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="5ec86-146">Занимает около 20 минут toocreate hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="5ec86-147">После создания ресурсов hello предпринимается колонки группы ресурсов перенаправленный toohello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="5ec86-149">Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ spark** и **базовое имя kafka**, где базовое имя — имя hello указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="5ec86-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="5ec86-150">Использовать эти имена на последующих этапах при подключении toohello кластеров.</span><span class="sxs-lookup"><span data-stu-id="5ec86-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="5ec86-151">Получить hello Kafka брокеров</span><span class="sxs-lookup"><span data-stu-id="5ec86-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="5ec86-152">Hello кода в этом примере подключается toohello Kafka компонента service broker узлов в кластере Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="5ec86-153">toofind hello Kafka узлов брокера, выполните следующий пример PowerShell или Bash hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

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
> <span data-ttu-id="5ec86-154">В этом примере ожидает `$PASSWORD` toocontain hello пароль для имени входа кластера hello, и `$CLUSTERNAME` toocontain имя hello hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="5ec86-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="5ec86-155">В этом примере используется hello [jq](https://stedolan.github.io/jq/) программа tooparse данных из документа JSON hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="5ec86-156">Hello выходных данных аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="5ec86-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="5ec86-157">Сохраните эти сведения, так как он используется в следующих разделах данного документа hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="5ec86-158">Получить записных книжек hello</span><span class="sxs-lookup"><span data-stu-id="5ec86-158">Get hello notebooks</span></span>

<span data-ttu-id="5ec86-159">Hello код для примера hello, описанные в этом документе доступен на [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="5ec86-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="5ec86-160">Отправка записных книжек hello</span><span class="sxs-lookup"><span data-stu-id="5ec86-160">Upload hello notebooks</span></span>

<span data-ttu-id="5ec86-161">Используйте следующую записных книжек hello tooupload действия из проекта hello tooyour Spark в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="5ec86-162">В веб-браузере подключитесь записной книжки Jupyter toohello на свой кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="5ec86-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="5ec86-163">В hello URL-адреса, замените `CLUSTERNAME` с именем hello Kafka кластера:</span><span class="sxs-lookup"><span data-stu-id="5ec86-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="5ec86-164">При появлении запроса введите hello кластера входа (для администратора) и пароль, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5ec86-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="5ec86-165">Hello верхней правой части страницы приветствия, с помощью hello __отправить__ hello tooupload кнопку __поток-Твиты-To_Kafka.ipynb__ файл toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="5ec86-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="5ec86-166">Выберите __откройте__ toostart hello передачи.</span><span class="sxs-lookup"><span data-stu-id="5ec86-166">Select __Open__ toostart hello upload.</span></span>

    ![Использовать tooselect кнопка отправки hello и отправка записной книжке](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Выберите файл KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="5ec86-169">Найти hello __поток-Твиты-To_Kafka.ipynb__ запись в списке hello портативные компьютеры, а затем выберите __отправить__ кнопку рядом с ней.</span><span class="sxs-lookup"><span data-stu-id="5ec86-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Используйте hello передачи рядом hello KafkaStreaming.ipynb входа tooupload его toohello записной книжки сервера](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="5ec86-171">Повторите шаги 1 – 3 hello tooload __Spark-структурированный-потоковой передачи-в-Kafka.ipynb__ ноутбука.</span><span class="sxs-lookup"><span data-stu-id="5ec86-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="5ec86-172">Загрузка твитов в Kafka</span><span class="sxs-lookup"><span data-stu-id="5ec86-172">Load tweets into Kafka</span></span>

<span data-ttu-id="5ec86-173">После загрузки файлов hello выберите hello __поток-Твиты-To_Kafka.ipynb__ записной книжки hello tooopen входа.</span><span class="sxs-lookup"><span data-stu-id="5ec86-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="5ec86-174">Выполните действия hello hello записной книжки tooload твиты в Kafka.</span><span class="sxs-lookup"><span data-stu-id="5ec86-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="5ec86-175">Обработка твитов с помощью структурированной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="5ec86-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="5ec86-176">Hello книжке Jupyter домашнюю страницу, выберите hello __Spark-структурированный-потоковой передачи-в-Kafka.ipynb__ входа.</span><span class="sxs-lookup"><span data-stu-id="5ec86-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="5ec86-177">Выполните действия hello hello записной книжки tooload твиты из Kafka, с помощью потоковой передачи структурированных Spark.</span><span class="sxs-lookup"><span data-stu-id="5ec86-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ec86-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ec86-178">Next steps</span></span>

<span data-ttu-id="5ec86-179">Теперь, когда вы узнали, как toouse Spark структурированных потоковой передачи, см. следующие дополнительные сведения о работе с Spark и Kafka toolearn документы hello:</span><span class="sxs-lookup"><span data-stu-id="5ec86-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="5ec86-180">[Как toouse усилить потоковой передачи (DStream) с Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="5ec86-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* <span data-ttu-id="5ec86-181">[Начало работы с записной книжкой Jupyter и Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5ec86-181">[Start with Jupyter Notebook and Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)</span></span>