---
title: "Потоковая передача Apache Spark и Kafka в Azure HDInsight | Документация Майкрософт"
description: "Узнайте об использовании Apache Spark для двунаправленного потокового обмена данными с Apache Kafka с помощью DStreams. В этом примере описано, как выполнить потоковую передачу данных, используя записную книжку Jupyter из Spark в HDInsight."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="8b475-105">Пример потоковой передачи Apache Spark (DStream) с использованием Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b475-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="8b475-106">Узнайте об использовании Apache Spark для двунаправленного потокового обмена данными с Apache Kafka в HDInsight с помощью DStreams.</span><span class="sxs-lookup"><span data-stu-id="8b475-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="8b475-107">В этом примере используется записная книжка Jupyter, которая выполняется на кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="8b475-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="8b475-108">Вы узнаете, как создать группу ресурсов Azure, которая содержит кластеры Spark и Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b475-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="8b475-109">Оба этих кластера находятся в виртуальной сети Azure, что позволяет кластеру Spark напрямую обмениваться данными с кластером Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="8b475-110">Выполнив инструкции, не забудьте удалить кластеры, чтобы избежать ненужных расходов.</span><span class="sxs-lookup"><span data-stu-id="8b475-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="8b475-111">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="8b475-111">Create the clusters</span></span>

<span data-ttu-id="8b475-112">Apache Kafka в HDInsight не предоставляет доступ к брокерам Kafka через общедоступный сегмент Интернета.</span><span class="sxs-lookup"><span data-stu-id="8b475-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="8b475-113">Все объекты, обращающиеся к Kafka, должны находиться в той же виртуальной сети Azure, что и узлы в кластере Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="8b475-114">В этом примере кластеры Kafka и Spark расположены в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="8b475-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="8b475-115">На следующей схеме показано, как взаимодействуют кластеры.</span><span class="sxs-lookup"><span data-stu-id="8b475-115">The following diagram shows how communication flows between the clusters:</span></span>

![Схема кластеров Spark и Kafka в виртуальной сети Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="8b475-117">Хотя само решение Kafka ограничено связью в пределах виртуальной сети, другие службы в кластере, например SSH и Ambari, доступны через Интернет.</span><span class="sxs-lookup"><span data-stu-id="8b475-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="8b475-118">Дополнительные сведения об общих портах, доступных в HDInsight, см. в статье [Порты и универсальные коды ресурсов (URI), используемые кластерами HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="8b475-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="8b475-119">Хотя виртуальную сеть Azure, а также кластеры Kafka и Spark можно создать вручную, проще использовать шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b475-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="8b475-120">Выполните следующие действия, чтобы развернуть виртуальную сеть Azure, а также кластеры Kafka и Spark в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="8b475-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="8b475-121">Нажмите эту кнопку, чтобы войти в Azure и открыть шаблон на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b475-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="8b475-122">Шаблон Azure Resource Manager находится здесь: **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="8b475-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8b475-123">Чтобы обеспечить доступность Kafka в HDInsight, кластер должен содержать не менее трех рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="8b475-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="8b475-124">Этот шаблон создает кластер Kafka, содержащий три рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="8b475-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="8b475-125">Этот шаблон создает кластер HDInsight 3.6 для Kafka и Spark.</span><span class="sxs-lookup"><span data-stu-id="8b475-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="8b475-126">Используйте следующие сведения, чтобы заполнить колонку **Настраиваемое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="8b475-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="8b475-128">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="8b475-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="8b475-129">Эта группа содержит кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b475-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="8b475-130">**Расположение.** Выберите близкое к вам географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="8b475-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="8b475-131">**Базовое имя кластера**. Это значение будет использоваться в качестве базового имени для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="8b475-132">Например, если ввести **hdi**, будет создан кластер Spark с именем spark-hdi__ и кластер Kafka с именем **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="8b475-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="8b475-133">**Cluster Login User Name** (Имя пользователя для входа в кластер). Имя администратора для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="8b475-134">**Cluster Login User Password** (Пароль пользователя для входа в кластер). Имя администратора для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="8b475-135">**Имя пользователя SSH.** Создаваемый пользователь SSH для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="8b475-136">**Пароль SSH.** Пароль пользователя SSH для кластеров Spark и Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="8b475-137">Прочтите **условия использования** и установите флажок **Я принимаю указанные выше условия**.</span><span class="sxs-lookup"><span data-stu-id="8b475-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="8b475-138">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="8b475-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="8b475-139">Процесс создания кластеров занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="8b475-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="8b475-140">Когда указанные ресурсы будут созданы, отобразится колонка группы ресурсов, которая содержит кластеры и веб-панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8b475-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Колонка группы ресурсов для виртуальной сети и кластеров](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="8b475-142">Обратите внимание, что кластерам HDInsight присвоены имена **spark-BASENAME** и **kafka-BASENAME**, где BASENAME — имя, указанное в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="8b475-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="8b475-143">Эти имена будут использоваться позже при подключении к кластерам.</span><span class="sxs-lookup"><span data-stu-id="8b475-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="8b475-144">Использование записных книжек</span><span class="sxs-lookup"><span data-stu-id="8b475-144">Use the notebooks</span></span>

<span data-ttu-id="8b475-145">Код для примера, описанного в этом документе, доступен по адресу [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="8b475-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="8b475-146">Следуйте указаниям в файле `README.md`, чтобы выполнить этот пример.</span><span class="sxs-lookup"><span data-stu-id="8b475-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="8b475-147">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="8b475-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="8b475-148">Выполнив описанные здесь инструкции, вы создадите два кластера в одной группе ресурсов Azure. Следовательно, вы можете удалить эту группу ресурсов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b475-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="8b475-149">При этом будут удалены все созданные в рамках этого руководства и используемые в кластерах ресурсы, виртуальная сеть Azure и учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="8b475-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b475-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b475-150">Next steps</span></span>

<span data-ttu-id="8b475-151">В этом примере описано, как использовать Spark для чтения и записи данных в Kafka.</span><span class="sxs-lookup"><span data-stu-id="8b475-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="8b475-152">Другие материалы, посвященные работе с Kafka, доступны по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="8b475-152">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="8b475-153">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="8b475-153">[Get started with Apache Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* <span data-ttu-id="8b475-154">[Use MirrorMaker to create a replica of a Kafka on HDInsight cluster (preview)](hdinsight-apache-kafka-mirroring.md) (Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="8b475-154">[Use MirrorMaker to create a replica of Kafka on HDInsight](hdinsight-apache-kafka-mirroring.md)</span></span>
* [<span data-ttu-id="8b475-155">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b475-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

