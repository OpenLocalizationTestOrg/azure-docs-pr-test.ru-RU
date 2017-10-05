---
title: "Структурированная потоковая передача Apache Spark с Kafka в Azure HDInsight | Документы Майкрософт"
description: "Узнайте об использовании потоковой передачи Apache Spark (DStream) для двунаправленного обмена данными с Apache Kafka. В этом примере показано, как выполнить потоковую передачу данных, используя записную книжку Jupyter из Spark в HDInsight."
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
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="bdb5f-104">Использование структурированной потоковой передачи Spark с Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdb5f-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="bdb5f-105">Узнайте, как использовать структурированную потоковую передачу Spark для чтения данных из Apache Kafka в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="bdb5f-106">Структурированная потоковая передача Spark — это механизм обработки потока, встроенный в Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="bdb5f-107">Он позволяет выражать потоковые вычисления так же, как пакетные вычисления статических данных.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="bdb5f-108">Дополнительные сведения о структурированной потоковой передаче см. в разделе [Руководство по программированию структурированной потоковой передачи [альфа-версия]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) на Apache.org.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdb5f-109">В этом примере используется Spark 2.1 в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="bdb5f-110">Структурированная потоковая передача рассматривается как __альфа-версия__ в Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="bdb5f-111">Вы узнаете, как создать группу ресурсов Azure, которая содержит кластеры Spark и Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="bdb5f-112">Оба этих кластера находятся в виртуальной сети Azure, что позволяет кластеру Spark напрямую обмениваться данными с кластером Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="bdb5f-113">Выполнив инструкции, не забудьте удалить кластеры, чтобы избежать ненужных расходов.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="bdb5f-114">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="bdb5f-114">Create the clusters</span></span>

<span data-ttu-id="bdb5f-115">Apache Kafka в HDInsight не предоставляет доступ к брокерам Kafka через общедоступный сегмент Интернета.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="bdb5f-116">Все объекты, обращающиеся к Kafka, должны находиться в той же виртуальной сети Azure, что и узлы в кластере Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="bdb5f-117">В этом примере кластеры Kafka и Spark расположены в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="bdb5f-118">На следующей схеме показано, как взаимодействуют кластеры.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-118">The following diagram shows how communication flows between the clusters:</span></span>

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="bdb5f-120">Служба Kafka ограничена обменом данными в пределах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="bdb5f-121">Другие службы в кластере, например SSH и Ambari, могут быть доступны через Интернет.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="bdb5f-122">Дополнительные сведения об общих портах, доступных в HDInsight, см. в статье [Порты и универсальные коды ресурсов (URI), используемые кластерами HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="bdb5f-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="bdb5f-123">Хотя виртуальную сеть Azure, а также кластеры Kafka и Spark можно создать вручную, проще использовать шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="bdb5f-124">Выполните следующие действия, чтобы развернуть виртуальную сеть Azure, а также кластеры Kafka и Spark в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="bdb5f-125">Нажмите эту кнопку, чтобы войти в Azure и открыть шаблон на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="bdb5f-126">Шаблон Azure Resource Manager находится здесь: **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="bdb5f-127">Этот шаблон создает следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="bdb5f-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="bdb5f-128">Kafka в кластере HDInsight 3.5;</span><span class="sxs-lookup"><span data-stu-id="bdb5f-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="bdb5f-129">Spark в кластере HDInsight 3.6;</span><span class="sxs-lookup"><span data-stu-id="bdb5f-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="bdb5f-130">виртуальную сеть Azure, содержащую кластеры HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bdb5f-131">Записная книжка структурированной потоковой передачи, используемая в этом примере, требует Spark в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="bdb5f-132">Если используется более ранняя версия Spark в HDInsight, возникнут ошибки при использовании этой записной книжки.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="bdb5f-133">Используйте следующие сведения, чтобы заполнить колонку **Настраиваемое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="bdb5f-135">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="bdb5f-136">Эта группа содержит кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="bdb5f-137">**Расположение.** Выберите близкое к вам географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="bdb5f-138">**Базовое имя кластера**. Это значение будет использоваться в качестве базового имени для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="bdb5f-139">Например, если ввести **hdi**, будет создан кластер Spark с именем spark-hdi__ и кластер Kafka с именем **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="bdb5f-140">**Cluster Login User Name** (Имя пользователя для входа в кластер). Имя администратора для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bdb5f-141">**Cluster Login User Password** (Пароль пользователя для входа в кластер). Имя администратора для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bdb5f-142">**Имя пользователя SSH.** Создаваемый пользователь SSH для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="bdb5f-143">**Пароль SSH.** Пароль пользователя SSH для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="bdb5f-144">Прочтите **условия использования** и установите флажок **Я принимаю указанные выше условия**.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="bdb5f-145">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="bdb5f-146">Процесс создания кластеров занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="bdb5f-147">После создания ресурсов вы будете перенаправлены в колонку группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Колонка группы ресурсов для виртуальной сети и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="bdb5f-149">Обратите внимание, что кластерам HDInsight присвоены имена **spark-BASENAME** и **kafka-BASENAME**, где BASENAME — имя, указанное в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="bdb5f-150">Эти имена будут использоваться позже при подключении к кластерам.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="bdb5f-151">Получение брокеров Kafka</span><span class="sxs-lookup"><span data-stu-id="bdb5f-151">Get the Kafka brokers</span></span>

<span data-ttu-id="bdb5f-152">Код в этом примере подключается к узлам брокера Kafka в кластере Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="bdb5f-153">Чтобы найти узлы брокера Kafka, используйте следующий пример PowerShell или Bash.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
> <span data-ttu-id="bdb5f-154">В этом примере предполагается, что `$PASSWORD` содержит пароль для входа в кластер, а `$CLUSTERNAME` содержит имя кластера Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="bdb5f-155">В этом примере используется служебная программа [jq](https://stedolan.github.io/jq/) для анализа данных из документа JSON.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="bdb5f-156">Результат будет аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="bdb5f-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="bdb5f-157">Сохраните эти сведения, так как они вам понадобятся в следующих разделах этого документа.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="bdb5f-158">Получение записных книжек</span><span class="sxs-lookup"><span data-stu-id="bdb5f-158">Get the notebooks</span></span>

<span data-ttu-id="bdb5f-159">Код для примера, описанного в этом документе, доступен по адресу [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="bdb5f-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="bdb5f-160">Отправка записных книжек</span><span class="sxs-lookup"><span data-stu-id="bdb5f-160">Upload the notebooks</span></span>

<span data-ttu-id="bdb5f-161">Чтобы отправить записные книжки из проекта в кластер Spark в HDInsight, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="bdb5f-162">В веб-браузере подключитесь к записной книжке Jupyter в вашем кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="bdb5f-163">В следующем URL-адресе замените `CLUSTERNAME` на имя вашего кластера Kafka:</span><span class="sxs-lookup"><span data-stu-id="bdb5f-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="bdb5f-164">При появлении запроса введите имя администратора кластера и пароль, которые использовались при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="bdb5f-165">В правой верхней части страницы нажмите кнопку __Отправить__, чтобы отправить файл __Stream-Tweets-To_Kafka.ipynb__ в кластер.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="bdb5f-166">Нажмите __Открыть__ для запуска отправки.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-166">Select __Open__ to start the upload.</span></span>

    ![Использование кнопки "Отправить" для выбора и загрузки блокнота](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Выбор файла KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="bdb5f-169">Найдите запись __Stream-Tweets-To_Kafka.ipynb__ в списке записных книжек, а затем нажмите расположенную рядом кнопку __Отправка__.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Использование кнопки "Отправка" рядом с записью KafkaStreaming.ipynb для отправки на сервер Jupyter Notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="bdb5f-171">Повторите шаги 1–3 для загрузки записной книжки __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="bdb5f-172">Загрузка твитов в Kafka</span><span class="sxs-lookup"><span data-stu-id="bdb5f-172">Load tweets into Kafka</span></span>

<span data-ttu-id="bdb5f-173">После отправки файлов выберите запись __Stream-Tweets-To_Kafka.ipynb__, чтобы открыть записную книжку.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="bdb5f-174">Выполните действия в записной книжке, чтобы загрузить твиты в Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="bdb5f-175">Обработка твитов с помощью структурированной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="bdb5f-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="bdb5f-176">На домашней странице записной книжки Jupyter выберите запись __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="bdb5f-177">Выполните действия в записной книжке, чтобы загрузить твиты из Kafka с помощью структурированной потоковой передачи Spark.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdb5f-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bdb5f-178">Next steps</span></span>

<span data-ttu-id="bdb5f-179">Теперь, когда вы узнали, как использовать структурированную потоковую передачу Spark, перейдите к следующим документам для углубленного изучения работы со Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="bdb5f-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="bdb5f-180">[Как использовать потоковую передачу Spark (DStream) с Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="bdb5f-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* <span data-ttu-id="bdb5f-181">[Начало работы с записной книжкой Jupyter и Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bdb5f-181">[Start with Jupyter Notebook and Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)</span></span>