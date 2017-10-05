---
title: "Приступая к работе с Apache Kafka в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как создать кластер Apache Kafka в Azure HDInsight. Узнайте, как создать разделы, подписки и потребителей."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="97103-104">Приступая к работе с Apache Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97103-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="97103-105">Узнайте, как создать кластер [Apache Kafka](https://kafka.apache.org) и использовать его в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="97103-106">Kafka — это распределенная платформа потоковой передачи с открытым кодом, которая доступна в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="97103-107">Она часто используется как брокер сообщений, предоставляя такие же функциональные возможности, как и очередь сообщений типа "публикация-подписка".</span><span class="sxs-lookup"><span data-stu-id="97103-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="97103-108">Сейчас в HDInsight доступны две версии Kafka: 0.9.0 (HDInsight 3.4) и 0.10.0 (HDInsight 3.5 и 3.6).</span><span class="sxs-lookup"><span data-stu-id="97103-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="97103-109">В этой статье предполагается, что вы используете Kafka с версией HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="97103-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="97103-110">Создание кластера Kafka</span><span class="sxs-lookup"><span data-stu-id="97103-110">Create a Kafka cluster</span></span>

<span data-ttu-id="97103-111">Чтобы создать Kafka в кластере HDInsight, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="97103-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="97103-112">На [портале Azure](https://portal.azure.com) последовательно выберите элементы **+Создать**, **Аналитика** и **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="97103-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Создание кластера HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="97103-114">В колонке **Основные сведения** задайте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="97103-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="97103-115">**Имя кластера.** Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="97103-116">**Подписка.** Выберите нужную подписку.</span><span class="sxs-lookup"><span data-stu-id="97103-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="97103-117">**Имя пользователя для входа в кластер** и **Пароль для входа в кластер**. Имя для входа в кластер по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="97103-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="97103-118">Эти учетные данные используются для доступа к таким службам, как веб-интерфейс Ambari или REST API.</span><span class="sxs-lookup"><span data-stu-id="97103-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="97103-119">**Secure Shell (SSH) username** (Имя пользователя Secure Shell (SSH)). Имя для доступа к кластеру по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="97103-120">По умолчанию пароль совпадает с паролем для входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="97103-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="97103-121">**Группа ресурсов.** Группа ресурсов, в которой будет создан кластер.</span><span class="sxs-lookup"><span data-stu-id="97103-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="97103-122">**Расположение.** Регион Azure, в котором будет создан кластер.</span><span class="sxs-lookup"><span data-stu-id="97103-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![Выберите подписку.](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="97103-124">Выберите **Тип кластера** и в колонке **Конфигурация кластера** задайте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="97103-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="97103-125">**Тип кластера**: Kafka.</span><span class="sxs-lookup"><span data-stu-id="97103-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="97103-126">**Версия**: Kafka 0.10.0 (HDI 3.6).</span><span class="sxs-lookup"><span data-stu-id="97103-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="97103-127">**Ценовая категория кластера**: "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="97103-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="97103-128">Затем нажмите кнопку **Выбрать**, чтобы сохранить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="97103-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![Выбор типа кластера](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="97103-130">Выбрав тип кластера, нажмите кнопку __Выбрать__, чтобы установить выбранный тип.</span><span class="sxs-lookup"><span data-stu-id="97103-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="97103-131">Затем нажмите кнопку __Далее__, чтобы завершить настройку основных параметров.</span><span class="sxs-lookup"><span data-stu-id="97103-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="97103-132">В колонке **Хранилище** выберите или создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="97103-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="97103-133">Для действий, описанных в этом документе, в других полях этой колонки оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="97103-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="97103-134">Нажмите кнопку __Далее__, чтобы сохранить конфигурацию хранилища.</span><span class="sxs-lookup"><span data-stu-id="97103-134">Use the __Next__ button to save storage configuration.</span></span>

    ![Настройка параметров учетной записи хранения для HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="97103-136">Чтобы продолжить, в колонке __Приложения (необязательно)__ щелкните __Далее__.</span><span class="sxs-lookup"><span data-stu-id="97103-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="97103-137">Для этого примера приложения не требуются.</span><span class="sxs-lookup"><span data-stu-id="97103-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="97103-138">Чтобы продолжить, в колонке __Размер кластера__ щелкните __Далее__.</span><span class="sxs-lookup"><span data-stu-id="97103-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="97103-139">Чтобы обеспечить доступность Kafka в HDInsight, кластер должен содержать не менее трех рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="97103-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Определение размер кластера Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="97103-141">**Число дисков для каждой записи рабочего узла** определяет степень масштабируемости Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="97103-142">См. дополнительные сведения о [настройке объема хранилища и степени масштабируемости Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="97103-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="97103-143">Чтобы продолжить, в колонке __Дополнительные параметры__ щелкните __Далее__.</span><span class="sxs-lookup"><span data-stu-id="97103-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="97103-144">В колонке **Сводка** проверьте конфигурацию для кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="97103-145">Используйте ссылки __Изменить__, чтобы изменить неправильные параметры.</span><span class="sxs-lookup"><span data-stu-id="97103-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="97103-146">Наконец, нажмите кнопку "Создать" для создания кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Сводка по конфигурации кластера](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="97103-148">Операция создания кластера может занять до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="97103-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="97103-149">Подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="97103-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97103-150">При выполнении следующих шагов необходимо использовать клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="97103-151">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="97103-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="97103-152">На своем клиенте используйте SSH, чтобы подключиться к кластеру:</span><span class="sxs-lookup"><span data-stu-id="97103-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="97103-153">Замените **SSHUSER** именем пользователя SSH, указанным при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="97103-154">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="97103-155">При появлении запроса введите пароль, который используется для учетной записи SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="97103-156">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="97103-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="97103-157"><a id="getkafkainfo"></a>Получение сведений об узлах Zookeeper и брокера</span><span class="sxs-lookup"><span data-stu-id="97103-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="97103-158">Для работы с Kafka вам нужно предоставить данные о двух узлах: *Zookeeper* и *брокера*.</span><span class="sxs-lookup"><span data-stu-id="97103-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="97103-159">Эти узлы используются Kafka API и многими другими служебными программами, поставляемыми с платформой Kafka.</span><span class="sxs-lookup"><span data-stu-id="97103-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="97103-160">Ниже описано, как создать переменные среды, которые содержат сведения об узле.</span><span class="sxs-lookup"><span data-stu-id="97103-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="97103-161">Эти переменные используются в нашем примере далее.</span><span class="sxs-lookup"><span data-stu-id="97103-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="97103-162">Используя SSH-подключение к кластеру, выполните следующую команду, чтобы установить служебную программу `jq`.</span><span class="sxs-lookup"><span data-stu-id="97103-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="97103-163">Эта служебная программа используется для синтаксического анализа документов JSON. С ее помощью также удобно получать сведения об узле брокера.</span><span class="sxs-lookup"><span data-stu-id="97103-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="97103-164">Используйте следующие команды, чтобы набрать переменные среды на основе информации, полученной из Ambari.</span><span class="sxs-lookup"><span data-stu-id="97103-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="97103-165">В качестве значения параметра `CLUSTERNAME=` задайте имя кластера Kafka.</span><span class="sxs-lookup"><span data-stu-id="97103-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="97103-166">Замените `PASSWORD=` паролем администратора, который использовался при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="97103-167">Ниже приведен пример содержимого `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="97103-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="97103-168">Ниже приведен пример содержимого `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="97103-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="97103-169">Команда `cut` используется для сокращения списка узлов для двух записей узлов.</span><span class="sxs-lookup"><span data-stu-id="97103-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="97103-170">При создании объект-получателя или производителя Kafka не нужно предоставлять полный список узлов.</span><span class="sxs-lookup"><span data-stu-id="97103-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="97103-171">Учтите, что данные, возвращаемые этим сеансом, могут быть неточными.</span><span class="sxs-lookup"><span data-stu-id="97103-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="97103-172">Масштабирование кластера обычно сопровождается добавлением или удалением брокеров.</span><span class="sxs-lookup"><span data-stu-id="97103-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="97103-173">Если происходит сбой, и узел заменяется, имя узла также может измениться.</span><span class="sxs-lookup"><span data-stu-id="97103-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="97103-174">Чтобы получить допустимые значения, всегда следует извлекать сведения об узлах Zookeeper и брокера непосредственно перед их использованием.</span><span class="sxs-lookup"><span data-stu-id="97103-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="97103-175">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="97103-175">Create a topic</span></span>

<span data-ttu-id="97103-176">Kafka хранит потоки данных в категориях, называемых *разделами*.</span><span class="sxs-lookup"><span data-stu-id="97103-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="97103-177">Чтобы создать такой раздел, запустите скрипт, который поставляется с Kafka, используя SSH-подключение к головному узлу кластера:</span><span class="sxs-lookup"><span data-stu-id="97103-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="97103-178">Эта команда создает подключение к Zookeeper, используя хранящиеся в `$KAFKAZKHOSTS` сведения об узле, а затем создает раздел Kafka с именем **test**.</span><span class="sxs-lookup"><span data-stu-id="97103-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="97103-179">Чтобы убедиться, что раздел создан, используйте следующий скрипт, который отображает список разделов.</span><span class="sxs-lookup"><span data-stu-id="97103-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="97103-180">В выходных данных этой команды перечислены разделы Kafka, среди которых должен быть и новый раздел **test**.</span><span class="sxs-lookup"><span data-stu-id="97103-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="97103-181">Создание и использование записей</span><span class="sxs-lookup"><span data-stu-id="97103-181">Produce and consume records</span></span>

<span data-ttu-id="97103-182">Kafka хранит *записи* в разделах.</span><span class="sxs-lookup"><span data-stu-id="97103-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="97103-183">Записи создаются *производителями*, а используются *потребителями*.</span><span class="sxs-lookup"><span data-stu-id="97103-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="97103-184">Производители извлекают записи из *брокеров* Kafka.</span><span class="sxs-lookup"><span data-stu-id="97103-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="97103-185">Каждый рабочий узел в кластере HDInsight — это брокер Kafka.</span><span class="sxs-lookup"><span data-stu-id="97103-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="97103-186">Ниже описано, как сначала сохранить записи в созданный ранее тестовый раздел, а затем считать их с помощью потребителя.</span><span class="sxs-lookup"><span data-stu-id="97103-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="97103-187">Запустите сеанс SSH и выполните скрипт, предоставленный службой Kafka для сохранения записей в раздел:</span><span class="sxs-lookup"><span data-stu-id="97103-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="97103-188">Эта команда не возвращает запрос после запуска.</span><span class="sxs-lookup"><span data-stu-id="97103-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="97103-189">Вместо этого введите несколько текстовых сообщений, а затем нажмите клавиши **Ctrl+C**, чтобы остановить отправку данных в раздел.</span><span class="sxs-lookup"><span data-stu-id="97103-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="97103-190">Каждая строка отправляется как отдельная запись.</span><span class="sxs-lookup"><span data-stu-id="97103-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="97103-191">Используйте скрипт, поставляемый с платформой Kafka, чтобы считать записи из раздела:</span><span class="sxs-lookup"><span data-stu-id="97103-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="97103-192">Эта команда извлекает записи из раздела, а затем отображает их.</span><span class="sxs-lookup"><span data-stu-id="97103-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="97103-193">Параметр `--from-beginning` указывает потребителю считывать данные с самого начала потока, поэтому будут извлечены все записи.</span><span class="sxs-lookup"><span data-stu-id="97103-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="97103-194">Нажмите клавиши __Ctrl+C__, чтобы остановить потребитель.</span><span class="sxs-lookup"><span data-stu-id="97103-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="97103-195">API производителя и потребителя</span><span class="sxs-lookup"><span data-stu-id="97103-195">Producer and consumer API</span></span>

<span data-ttu-id="97103-196">Вы также можете создавать и использовать записи программным способом — с помощью [API-интерфейсов Kafka](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="97103-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="97103-197">Чтобы создать производитель и объект-получатель Java, выполните следующие действия в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="97103-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97103-198">В среде разработки необходимо установить следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="97103-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="97103-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или эквивалент, например OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="97103-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="97103-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="97103-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="97103-201">Клиент SSH и команда `scp`.</span><span class="sxs-lookup"><span data-stu-id="97103-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="97103-202">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="97103-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="97103-203">Скачайте примеры на странице [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="97103-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="97103-204">В примере с производителем и потребителем используется проект в каталоге `Producer-Consumer`.</span><span class="sxs-lookup"><span data-stu-id="97103-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="97103-205">В примере ниже используются следующие классы.</span><span class="sxs-lookup"><span data-stu-id="97103-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="97103-206">**Run** — запускает потребителя или производителя.</span><span class="sxs-lookup"><span data-stu-id="97103-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="97103-207">**Producer** — сохраняет 1 000 000 записей в раздел.</span><span class="sxs-lookup"><span data-stu-id="97103-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="97103-208">**Consumer** — считывает записи из раздела.</span><span class="sxs-lookup"><span data-stu-id="97103-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="97103-209">Измените путь к каталогам на расположение каталога `Producer-Consumer` с примером. Затем используйте следующую команду, чтобы создать пакет JAR:</span><span class="sxs-lookup"><span data-stu-id="97103-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="97103-210">Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="97103-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="97103-211">С помощью следующих команд скопируйте файл `kafka-producer-consumer-1.0-SNAPSHOT.jar` в свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="97103-212">Замените **SSHUSER** именем пользователя SSH для кластера, а **CLUSTERNAME** — именем кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="97103-213">При появлении запроса введите пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="97103-214">Когда команда `scp` закончит копирование файла, подключитесь к кластеру с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="97103-215">Для записи в тестовый раздел используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="97103-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="97103-216">Когда процесс завершится, используйте следующую команду для считывания записей из раздела:</span><span class="sxs-lookup"><span data-stu-id="97103-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="97103-217">Отобразятся считанные записи, а также их количество.</span><span class="sxs-lookup"><span data-stu-id="97103-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="97103-218">Вы можете увидеть, что в разделе сохранено больше 1 000 000 записей, так как ранее мы уже отправили несколько записей с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="97103-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="97103-219">Нажмите клавиши __Ctrl+C__, чтобы закрыть потребитель.</span><span class="sxs-lookup"><span data-stu-id="97103-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="97103-220">Несколько потребителей</span><span class="sxs-lookup"><span data-stu-id="97103-220">Multiple consumers</span></span>

<span data-ttu-id="97103-221">При считывании записей объект-получатель Kafka использует группу объектов-получателей.</span><span class="sxs-lookup"><span data-stu-id="97103-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="97103-222">Использование одной группы с несколькими потребителями приведет к считыванию записей с балансировкой нагрузки из раздела.</span><span class="sxs-lookup"><span data-stu-id="97103-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="97103-223">Каждый потребитель в группе получает часть записей.</span><span class="sxs-lookup"><span data-stu-id="97103-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="97103-224">Увидеть это в действии можно так:</span><span class="sxs-lookup"><span data-stu-id="97103-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="97103-225">Откройте еще один сеанс SSH в кластере (сеансов должно быть два).</span><span class="sxs-lookup"><span data-stu-id="97103-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="97103-226">В каждом сеансе используйте следующую команду, чтобы запустить объект-получатель с идентификатором группы объектов-получателей:</span><span class="sxs-lookup"><span data-stu-id="97103-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="97103-227">Эта команда запускает объект-получатель с помощью идентификатора группы `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="97103-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97103-228">Используйте команды, приведенные в разделе [Получение сведений об узлах Zookeeper и брокера](#getkafkainfo), чтобы определить `$KAFKABROKERS` для этого сеанса SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="97103-229">Вы увидите, как каждый сеанс отображает число записей, получаемых из раздела.</span><span class="sxs-lookup"><span data-stu-id="97103-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="97103-230">Общее число, полученное в двух сеансах, должно совпадать с ранее полученным числом от одного потребителя.</span><span class="sxs-lookup"><span data-stu-id="97103-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="97103-231">Потребление по клиентам, входящих в одну группу, обрабатывается по секциям раздела.</span><span class="sxs-lookup"><span data-stu-id="97103-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="97103-232">Созданный ранее раздел `test` содержит восемь секций.</span><span class="sxs-lookup"><span data-stu-id="97103-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="97103-233">Если открыть восемь сеансов SSH и запустить в них потребителей, каждый потребитель будет считывать записи из одной секции этого раздела.</span><span class="sxs-lookup"><span data-stu-id="97103-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97103-234">Число экземпляров потребителя, входящих в группу потребителей, должно соответствовать числу секций.</span><span class="sxs-lookup"><span data-stu-id="97103-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="97103-235">В этом примере одна группа объектов-получателей может содержать не больше восьми объектов-получателей, так как это число секций в разделе.</span><span class="sxs-lookup"><span data-stu-id="97103-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="97103-236">Но у вас может быть несколько групп объектов-получателей, в каждую из которых входит не более восьми из них.</span><span class="sxs-lookup"><span data-stu-id="97103-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="97103-237">Записи хранятся в Kafka в том порядке, в котором они поступают в секцию.</span><span class="sxs-lookup"><span data-stu-id="97103-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="97103-238">Чтобы обеспечить упорядоченную доставку записей *в секцию*, нужно создать группу потребителей. При этом число входящих в нее экземпляров потребителя должно соответствовать числу секций.</span><span class="sxs-lookup"><span data-stu-id="97103-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="97103-239">Чтобы обеспечить упорядоченную доставку записей *в раздел*, нужно создать группу потребителей, которая содержит только один экземпляр потребителя.</span><span class="sxs-lookup"><span data-stu-id="97103-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="97103-240">API для потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="97103-240">Streaming API</span></span>

<span data-ttu-id="97103-241">API для потоковой передачи реализован в версии Kafka 0.10.0. В более ранних выпусках для обработки потоков используются Apache Spark или Storm.</span><span class="sxs-lookup"><span data-stu-id="97103-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="97103-242">При необходимости скачайте примеры на странице [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) и сохраните их в своей среде разработки.</span><span class="sxs-lookup"><span data-stu-id="97103-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="97103-243">В этом примере потоковой передачи используется проект в каталоге `streaming`.</span><span class="sxs-lookup"><span data-stu-id="97103-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="97103-244">Этот проект содержит только один класс `Stream`, который считывает данные из ранее созданного раздела `test`.</span><span class="sxs-lookup"><span data-stu-id="97103-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="97103-245">Он подсчитывает считанные слова, передавая каждое слово и их число в раздел с именем `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="97103-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="97103-246">(Раздел `wordcounts` в нашем примере создается позже.)</span><span class="sxs-lookup"><span data-stu-id="97103-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="97103-247">Из командной строки в среде разработки измените путь к каталогам на расположение каталога `Streaming`. Затем используйте следующую команду, чтобы создать пакет JAR.</span><span class="sxs-lookup"><span data-stu-id="97103-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="97103-248">Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="97103-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="97103-249">С помощью следующих команд скопируйте файл `kafka-streaming-1.0-SNAPSHOT.jar` в свой кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="97103-250">Замените **SSHUSER** именем пользователя SSH для кластера, а **CLUSTERNAME** — именем кластера.</span><span class="sxs-lookup"><span data-stu-id="97103-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="97103-251">При появлении запроса введите пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="97103-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="97103-252">Когда команда `scp` завершит копирование файла, подключитесь к кластеру по протоколу SSH. Затем используйте следующую команду, чтобы создать раздел `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="97103-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="97103-253">Теперь запустите процесс потоковой передачи с помощью приведенной ниже команды.</span><span class="sxs-lookup"><span data-stu-id="97103-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="97103-254">Потоковая передача будет запущена в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="97103-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="97103-255">Используйте следующую команду для отправки сообщений в раздел `test`.</span><span class="sxs-lookup"><span data-stu-id="97103-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="97103-256">В рамках потоковой передачи начнется их обработка:</span><span class="sxs-lookup"><span data-stu-id="97103-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="97103-257">Используйте приведенную ниже команду для просмотра выходных данных, записанных в раздел `wordcounts` процессом потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="97103-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="97103-258">Чтобы просмотреть данные, необходимо указать потребителю вывести ключ (который содержит значение) и десериализатор.</span><span class="sxs-lookup"><span data-stu-id="97103-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="97103-259">Имя ключа — это слово, а значение ключа содержит число.</span><span class="sxs-lookup"><span data-stu-id="97103-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="97103-260">Результат будет аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="97103-260">The output is similar to the following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="97103-261">Число увеличивается каждый раз, когда в сообщении встречается слово.</span><span class="sxs-lookup"><span data-stu-id="97103-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="97103-262">Нажмите клавиши __Ctrl+C__, чтобы закрыть потребитель, а затем с помощью команды `fg` выведите фоновую задачу потоковой передачи на передний план.</span><span class="sxs-lookup"><span data-stu-id="97103-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="97103-263">Для завершения работы также нажмите клавиши __Ctrl+C__.</span><span class="sxs-lookup"><span data-stu-id="97103-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="97103-264">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="97103-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="97103-265">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="97103-265">Troubleshoot</span></span>

<span data-ttu-id="97103-266">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="97103-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97103-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97103-267">Next steps</span></span>

<span data-ttu-id="97103-268">В этой статье описаны основные принципы работы с Apache Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97103-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="97103-269">Дополнительные сведения о работе с Kafka см. в следующих материалах.</span><span class="sxs-lookup"><span data-stu-id="97103-269">Use the following to learn more about working with Kafka:</span></span>

* <span data-ttu-id="97103-270">[High availability of your data with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-high-availability.md) (Высокий уровень доступности данных с Apache Kafka (предварительная версия) в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="97103-270">[Ensure high availability of your data with Kafka on HDInsight](hdinsight-apache-kafka-high-availability.md)</span></span>
* <span data-ttu-id="97103-271">[Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Настройка объема хранилища и степени масштабируемости для Apache Kafka в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="97103-271">[Increase scalability by configuring managed disks with Kafka on HDInsight](hdinsight-apache-kafka-scalability.md)</span></span>
* <span data-ttu-id="97103-272">[Документация по Apache Kafka](http://kafka.apache.org/documentation.html) на сайте kafka.apache.org</span><span class="sxs-lookup"><span data-stu-id="97103-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* <span data-ttu-id="97103-273">[Use MirrorMaker to create a replica of a Kafka on HDInsight cluster (preview)](hdinsight-apache-kafka-mirroring.md) (Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="97103-273">[Use MirrorMaker to create a replica of Kafka on HDInsight](hdinsight-apache-kafka-mirroring.md)</span></span>
* [<span data-ttu-id="97103-274">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97103-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="97103-275">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="97103-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="97103-276">Подключение к Kafka через виртуальную сеть Azure</span><span class="sxs-lookup"><span data-stu-id="97103-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
