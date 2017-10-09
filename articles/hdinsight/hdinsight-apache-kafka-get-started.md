---
title: "aaaStart с Kafka Apache - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Kafka Apache кластера в Azure HDInsight. Узнайте, как toocreate разделы, подписчиков и потребителей."
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
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="f790f-104">Приступая к работе с Apache Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f790f-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f790f-105">Узнайте, как toocreate и использовать [Apache Kafka](https://kafka.apache.org) кластера Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f790f-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="f790f-106">Kafka — это распределенная платформа потоковой передачи с открытым кодом, которая доступна в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f790f-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="f790f-107">Он часто используется как брокер обмена сообщениями, как она предоставляет функциональность, аналогичную tooa публикации подписки очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="f790f-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="f790f-108">Сейчас в HDInsight доступны две версии Kafka: 0.9.0 (HDInsight 3.4) и 0.10.0 (HDInsight 3.5 и 3.6).</span><span class="sxs-lookup"><span data-stu-id="f790f-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="f790f-109">Hello в этом документе предполагается, что вы используете Kafka на HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="f790f-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="f790f-110">Создание кластера Kafka</span><span class="sxs-lookup"><span data-stu-id="f790f-110">Create a Kafka cluster</span></span>

<span data-ttu-id="f790f-111">Используйте следующие шаги toocreate Kafka в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="f790f-112">Из hello [портал Azure](https://portal.azure.com)выберите **+ создать**, **аналитики + аналитика**, а затем выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f790f-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Создание кластера HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="f790f-114">Из **основы**, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="f790f-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="f790f-115">**Имя кластера**: hello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="f790f-116">**Подписки**: выберите toouse hello подписки.</span><span class="sxs-lookup"><span data-stu-id="f790f-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="f790f-117">**Кластер пользователя для входа** и **входа пароль кластера**: hello входа при доступе к hello кластера по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f790f-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="f790f-118">Можно использовать эти учетные данные tooaccess службы как hello Ambari веб-интерфейса или REST API.</span><span class="sxs-lookup"><span data-stu-id="f790f-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="f790f-119">**Secure Shell (SSH) username**: hello имя входа, используемое при доступе к hello кластера через SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="f790f-120">По умолчанию hello пароль является hello то же, что пароль имени входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="f790f-121">**Группа ресурсов**: hello ресурсов группы toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="f790f-122">**Расположение**: hello регион Azure toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Выберите подписку.](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="f790f-124">Выберите **кластера типа**, и выполнив hello набора значений из **конфигурации кластера**:</span><span class="sxs-lookup"><span data-stu-id="f790f-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="f790f-125">**Тип кластера**: Kafka.</span><span class="sxs-lookup"><span data-stu-id="f790f-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="f790f-126">**Версия**: Kafka 0.10.0 (HDI 3.6).</span><span class="sxs-lookup"><span data-stu-id="f790f-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="f790f-127">**Ценовая категория кластера**: "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="f790f-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="f790f-128">Наконец, используйте hello **выберите** кнопку toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="f790f-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Выбор типа кластера](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="f790f-130">После выбора типа hello кластера использовать hello __выберите__ tooset hello кластера тип кнопки.</span><span class="sxs-lookup"><span data-stu-id="f790f-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="f790f-131">Затем используйте hello __Далее__ кнопку toofinish базовой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f790f-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="f790f-132">В колонке **Хранилище** выберите или создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="f790f-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="f790f-133">Hello в данном пошаговом руководстве можно оставьте hello другие поля в значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="f790f-134">Используйте hello __Далее__ кнопку toosave хранилища конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f790f-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Задайте параметры учетной записи хранилища hello для HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="f790f-136">Из __приложения (необязательно)__выберите __Далее__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f790f-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="f790f-137">Для этого примера приложения не требуются.</span><span class="sxs-lookup"><span data-stu-id="f790f-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="f790f-138">Из __размер кластера__выберите __Далее__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f790f-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f790f-139">доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="f790f-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Набор hello Kafka размер кластера](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="f790f-141">Hello **дисков на рабочий узел** элементов управления для ввода hello масштабируемость Kafka на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f790f-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="f790f-142">См. дополнительные сведения о [настройке объема хранилища и степени масштабируемости Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="f790f-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="f790f-143">Из __Дополнительные параметры__выберите __Далее__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f790f-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="f790f-144">Из hello **Сводка**, проверьте конфигурацию hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="f790f-145">Используйте hello __изменить__ связывает toochange все параметры, которые являются неправильными.</span><span class="sxs-lookup"><span data-stu-id="f790f-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="f790f-146">Наконец используйте the__Create__ кнопку toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Сводка по конфигурации кластера](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="f790f-148">Он может занять too20 минут toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="f790f-149">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="f790f-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f790f-150">При выполнении hello, выполнив действия, необходимо использовать такой клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="f790f-151">Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="f790f-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="f790f-152">В клиентском приложении используйте SSH tooconnect toohello кластера:</span><span class="sxs-lookup"><span data-stu-id="f790f-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="f790f-153">Замените **SSHUSER** с именем пользователя SSH hello, указанный во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="f790f-154">Замените **CLUSTERNAME** с именем hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="f790f-155">При появлении запроса введите hello пароль, используемый для hello SSH учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f790f-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="f790f-156">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f790f-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="f790f-157"><a id="getkafkainfo"></a>Получение сведений узла Zookeeper и Broker hello</span><span class="sxs-lookup"><span data-stu-id="f790f-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="f790f-158">При работе с Kafka, необходимо знать два значения узла; Hello *Zookeeper* узлов и hello *Broker* узлов.</span><span class="sxs-lookup"><span data-stu-id="f790f-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="f790f-159">Эти узлы используются с hello Kafka API и многие hello программ, поставляемых вместе с Kafka.</span><span class="sxs-lookup"><span data-stu-id="f790f-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="f790f-160">Используйте следующие переменные среды toocreate шаги, которые содержат сведения об узле hello hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="f790f-161">Эти переменные используются в hello в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f790f-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="f790f-162">Из кластера toohello подключения SSH, используйте hello следующая команда tooinstall hello `jq` программы.</span><span class="sxs-lookup"><span data-stu-id="f790f-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="f790f-163">Эта программа используется tooparse документов JSON и используется при получении сведений о хосте broker hello:</span><span class="sxs-lookup"><span data-stu-id="f790f-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="f790f-164">переменные среды hello tooset сведениями получено из Ambari hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f790f-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f790f-165">Задать `CLUSTERNAME=` toohello имя hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="f790f-166">Задать `PASSWORD=` toohello пароль имени входа (для администратора), используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="f790f-167">Hello следующий текст является примером hello содержимое `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="f790f-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="f790f-168">Hello следующий текст является примером hello содержимое `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="f790f-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="f790f-169">Hello `cut` команда является список используемых tootrim hello записей узлов tootwo узлов.</span><span class="sxs-lookup"><span data-stu-id="f790f-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="f790f-170">Полный список tooprovide hello узлов не обязательно при создании потребителя Kafka или производителем.</span><span class="sxs-lookup"><span data-stu-id="f790f-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="f790f-171">Не следует полагаться на hello сведения, возвращаемые из этого сеанса tooalways быть точным.</span><span class="sxs-lookup"><span data-stu-id="f790f-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="f790f-172">При масштабировании кластера hello новый брокеры добавляются или удаляются.</span><span class="sxs-lookup"><span data-stu-id="f790f-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="f790f-173">Если происходит сбой и заменяется узла, может измениться hello имя узла для узла hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="f790f-174">Незадолго до его использовать tooensure имеют недопустимые данные, должны извлекать сведения hello Zookeeper и broker узлов.</span><span class="sxs-lookup"><span data-stu-id="f790f-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="f790f-175">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="f790f-175">Create a topic</span></span>

<span data-ttu-id="f790f-176">Kafka хранит потоки данных в категориях, называемых *разделами*.</span><span class="sxs-lookup"><span data-stu-id="f790f-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="f790f-177">В SSH подключения tooa кластера головному узлу используйте сценарий, в состав Kafka toocreate раздела:</span><span class="sxs-lookup"><span data-stu-id="f790f-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f790f-178">Эта команда устанавливает подключение с помощью узла hello, хранящихся в tooZookeeper `$KAFKAZKHOSTS`и затем создать Kafka раздел с именем **тестирования**.</span><span class="sxs-lookup"><span data-stu-id="f790f-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="f790f-179">Вы можете подтвердить эту статью hello был создан с помощью hello следующие статьи, посвященные toolist сценария:</span><span class="sxs-lookup"><span data-stu-id="f790f-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="f790f-180">Hello выходные данные этой команды список Kafka разделов, который содержит hello **тестирования** раздела.</span><span class="sxs-lookup"><span data-stu-id="f790f-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="f790f-181">Создание и использование записей</span><span class="sxs-lookup"><span data-stu-id="f790f-181">Produce and consume records</span></span>

<span data-ttu-id="f790f-182">Kafka хранит *записи* в разделах.</span><span class="sxs-lookup"><span data-stu-id="f790f-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="f790f-183">Записи создаются *производителями*, а используются *потребителями*.</span><span class="sxs-lookup"><span data-stu-id="f790f-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="f790f-184">Производители извлекают записи из *брокеров* Kafka.</span><span class="sxs-lookup"><span data-stu-id="f790f-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="f790f-185">Каждый рабочий узел в кластере HDInsight — это брокер Kafka.</span><span class="sxs-lookup"><span data-stu-id="f790f-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="f790f-186">Используйте следующие шаги toostore записи в разделе тестирования hello, созданной ранее и затем читать их с помощью объекта-получателя hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="f790f-187">Из сеанса SSH hello используйте сценарий, предоставленный службой Kafka toowrite записей toohello раздела:</span><span class="sxs-lookup"><span data-stu-id="f790f-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="f790f-188">Вы не возвращаются toohello запрос после этой команды.</span><span class="sxs-lookup"><span data-stu-id="f790f-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="f790f-189">Вместо этого введите несколько текстовых сообщений, а затем использовать **сочетание клавиш Ctrl + C** toostop отправки toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="f790f-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="f790f-190">Каждая строка отправляется как отдельная запись.</span><span class="sxs-lookup"><span data-stu-id="f790f-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="f790f-191">Используйте сценарий, в состав Kafka tooread записи из раздела hello:</span><span class="sxs-lookup"><span data-stu-id="f790f-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="f790f-192">Эта команда извлекает записи hello из раздела hello и отображает их.</span><span class="sxs-lookup"><span data-stu-id="f790f-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="f790f-193">С помощью `--from-beginning` сообщает toostart hello потребителя с начала hello hello потока, поэтому загружаются все записи.</span><span class="sxs-lookup"><span data-stu-id="f790f-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="f790f-194">Используйте __сочетание клавиш Ctrl + C__ toostop hello потребителя.</span><span class="sxs-lookup"><span data-stu-id="f790f-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="f790f-195">API производителя и потребителя</span><span class="sxs-lookup"><span data-stu-id="f790f-195">Producer and consumer API</span></span>

<span data-ttu-id="f790f-196">Вы можете также программно создавать и использовать записей с помощью hello [Kafka API-интерфейсы](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="f790f-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="f790f-197">toobuild Java производителя и потребителя, используйте hello, выполнив действия из среды разработки.</span><span class="sxs-lookup"><span data-stu-id="f790f-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f790f-198">Необходимо иметь следующие компоненты, установленные в среде разработки hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="f790f-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) или эквивалент, например OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f790f-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="f790f-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="f790f-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="f790f-201">SSH-клиента и hello `scp` команды.</span><span class="sxs-lookup"><span data-stu-id="f790f-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="f790f-202">Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="f790f-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="f790f-203">Загрузить примеры hello из [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="f790f-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="f790f-204">Например производителем и потребителем hello, используйте проект hello в hello `Producer-Consumer` каталога.</span><span class="sxs-lookup"><span data-stu-id="f790f-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="f790f-205">Данный пример содержит следующие классы hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="f790f-206">**Запустите** -начинается hello потребителя или производителем.</span><span class="sxs-lookup"><span data-stu-id="f790f-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="f790f-207">**Производитель** -раздел toohello 1 000 000 записей хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f790f-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="f790f-208">**Потребитель** -считывает записи из раздела hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="f790f-209">toocreate JAR-файл пакета, изменение расположения toohello каталоги hello `Producer-Consumer` hello каталог и использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f790f-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="f790f-210">Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f790f-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f790f-211">Используйте hello следующими командами toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` кластера HDInsight tooyour файла:</span><span class="sxs-lookup"><span data-stu-id="f790f-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="f790f-212">Замените **SSHUSER** пользователю hello SSH для кластера и замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="f790f-213">При появлении запроса введите пароль hello hello пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="f790f-214">Здравствуйте, один раз `scp` команды завершения копирования файла hello, подключите toohello кластер с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="f790f-215">Используйте следующие команды toowrite записей toohello тестировать раздел hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="f790f-216">После завершения процесса hello, используйте следующую команду tooread из раздела hello hello:</span><span class="sxs-lookup"><span data-stu-id="f790f-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="f790f-217">чтение, а также количество записей, записей Hello отображается.</span><span class="sxs-lookup"><span data-stu-id="f790f-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="f790f-218">Вы можете увидеть несколько более 1 000 000, регистрируются в журнале как отправлено несколько раздел toohello записи, с помощью скрипта на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="f790f-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="f790f-219">Используйте __сочетание клавиш Ctrl + C__ tooexit hello потребителя.</span><span class="sxs-lookup"><span data-stu-id="f790f-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="f790f-220">Несколько потребителей</span><span class="sxs-lookup"><span data-stu-id="f790f-220">Multiple consumers</span></span>

<span data-ttu-id="f790f-221">При считывании записей объект-получатель Kafka использует группу объектов-получателей.</span><span class="sxs-lookup"><span data-stu-id="f790f-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="f790f-222">Использование hello же группы с несколькими потребителями результаты нагрузки балансировки операций чтения из раздела.</span><span class="sxs-lookup"><span data-stu-id="f790f-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="f790f-223">Каждый пользователь в группе hello получает часть записей hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="f790f-224">toosee, этот процесс в действии hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="f790f-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="f790f-225">Открытие нового SSH сеанса toohello кластера, у вас есть два из них.</span><span class="sxs-lookup"><span data-stu-id="f790f-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="f790f-226">В каждом сеансе использовать hello следующие toostart потребителя с hello таким же Идентификатором группы потребителей:</span><span class="sxs-lookup"><span data-stu-id="f790f-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="f790f-227">Эта команда запускает объекта-получателя с помощью идентификатора группы hello `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="f790f-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f790f-228">Использование команд hello в hello [получить hello Zookeeper и Broker сведения об узле](#getkafkainfo) tooset раздел `$KAFKABROKERS` для этого сеанса SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="f790f-229">Смотрите, как каждый сеанс счетчики hello получаемые им записи из раздела hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="f790f-230">всего Hello обоих сеансов следует hello же, как ранее полученный от одного потребителя.</span><span class="sxs-lookup"><span data-stu-id="f790f-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="f790f-231">Использование клиентов в одной группе осуществляется при помощи hello секций для раздела hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="f790f-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="f790f-232">Для hello `test` раздел, созданный ранее, он имеет восемь секции.</span><span class="sxs-lookup"><span data-stu-id="f790f-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="f790f-233">Если открыть восьми сеансов SSH и запуска объекта-получателя во всех сеансах, каждый потребитель считывает записи из одной секции для раздела hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f790f-234">Число экземпляров потребителя, входящих в группу потребителей, должно соответствовать числу секций.</span><span class="sxs-lookup"><span data-stu-id="f790f-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="f790f-235">В этом примере одной группе потребителей может содержать вверх tooeight потребителей, так как это hello количество секций в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="f790f-236">Но у вас может быть несколько групп объектов-получателей, в каждую из которых входит не более восьми из них.</span><span class="sxs-lookup"><span data-stu-id="f790f-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="f790f-237">Записей, хранимых в Kafka хранятся в порядке hello, в котором они поступают в секции.</span><span class="sxs-lookup"><span data-stu-id="f790f-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="f790f-238">tooachieve в упорядоченной доставки для записей *внутри секции*, создать группу потребителей, где hello число экземпляров потребителя соответствует hello число секций.</span><span class="sxs-lookup"><span data-stu-id="f790f-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="f790f-239">tooachieve в упорядоченной доставки для записей *hello раздела*, создать группу потребителей с помощью только одного потребителя экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f790f-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="f790f-240">API для потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="f790f-240">Streaming API</span></span>

<span data-ttu-id="f790f-241">Hello потоковой передачи API была добавлена tooKafka в версии 0.10.0; более ранних версиях используют Apache Spark или ураган для обработки потока.</span><span class="sxs-lookup"><span data-stu-id="f790f-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="f790f-242">Если это еще не сделано, Загрузите примеры hello из [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour среды разработки.</span><span class="sxs-lookup"><span data-stu-id="f790f-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="f790f-243">Hello пример потоковой передачи, используйте проект hello в hello `streaming` каталога.</span><span class="sxs-lookup"><span data-stu-id="f790f-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="f790f-244">Этот проект содержит только один класс `Stream`, который считывает записи из hello `test` раздел создан ранее.</span><span class="sxs-lookup"><span data-stu-id="f790f-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="f790f-245">Он выполняет подсчет слов hello чтения и передает каждый tooa раздел word и счетчик с именем `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="f790f-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="f790f-246">Hello `wordcounts` раздел создается позднее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f790f-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="f790f-247">Из командной строки hello в среде разработки, изменить расположение каталогов toohello hello `Streaming` каталог, а затем используйте hello, следующая команда toocreate JAR-файл пакета:</span><span class="sxs-lookup"><span data-stu-id="f790f-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="f790f-248">Эта команда создает каталог с именем `target`, который содержит файл с именем `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f790f-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="f790f-249">Используйте hello следующими командами toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` кластера HDInsight tooyour файла:</span><span class="sxs-lookup"><span data-stu-id="f790f-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="f790f-250">Замените **SSHUSER** пользователю hello SSH для кластера и замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="f790f-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="f790f-251">При появлении запроса введите пароль hello hello пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="f790f-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="f790f-252">Здравствуйте, один раз `scp` команды завершения копирования файла hello, подключитесь toohello кластера с помощью SSH и воспользуйтесь hello, следующая команда toocreate hello `wordcounts` раздела:</span><span class="sxs-lookup"><span data-stu-id="f790f-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="f790f-253">Теперь можно запустите hello потоковой передачи процесса с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f790f-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="f790f-254">Эта команда запускает hello потоковой передачи процесса в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="f790f-255">Используйте hello следующая команда toohello сообщения toosend `test` раздела.</span><span class="sxs-lookup"><span data-stu-id="f790f-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="f790f-256">Эти сообщения обрабатываются hello пример потоковой передачи:</span><span class="sxs-lookup"><span data-stu-id="f790f-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="f790f-257">Используйте hello следующие выходные данные команды tooview hello записывается toohello `wordcounts` раздел по hello потоковой передачи процесса:</span><span class="sxs-lookup"><span data-stu-id="f790f-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="f790f-258">tooview hello данных, необходимо сообщить ключом hello tooprint hello и toouse десериализатор hello hello ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="f790f-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="f790f-259">Имя ключа Hello — слово hello и значение ключа hello содержится счетчик hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="f790f-260">Hello выходных данных аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="f790f-260">hello output is similar toohello following text:</span></span>
   
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
    > <span data-ttu-id="f790f-261">Hello счетчик увеличивается каждый раз, когда встречается слово.</span><span class="sxs-lookup"><span data-stu-id="f790f-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="f790f-262">Использовать hello __сочетание клавиш Ctrl + C__ tooexit hello потребителя, а затем использовать hello `fg` команда toobring hello потоковой передачи переднего плана задней toohello фоновой задачи.</span><span class="sxs-lookup"><span data-stu-id="f790f-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="f790f-263">Используйте __сочетание клавиш Ctrl + C__ tooexit он также.</span><span class="sxs-lookup"><span data-stu-id="f790f-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f790f-264">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="f790f-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="f790f-265">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f790f-265">Troubleshoot</span></span>

<span data-ttu-id="f790f-266">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f790f-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f790f-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f790f-267">Next steps</span></span>

<span data-ttu-id="f790f-268">В этом документе вы узнали основы работы с Apache Kafka на HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="f790f-269">Используйте следующие toolearn Дополнительные сведения о работе с Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="f790f-269">Use hello following toolearn more about working with Kafka:</span></span>

* <span data-ttu-id="f790f-270">[High availability of your data with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-high-availability.md) (Высокий уровень доступности данных с Apache Kafka (предварительная версия) в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f790f-270">[Ensure high availability of your data with Kafka on HDInsight](hdinsight-apache-kafka-high-availability.md)</span></span>
* <span data-ttu-id="f790f-271">[Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Настройка объема хранилища и степени масштабируемости для Apache Kafka в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f790f-271">[Increase scalability by configuring managed disks with Kafka on HDInsight](hdinsight-apache-kafka-scalability.md)</span></span>
* <span data-ttu-id="f790f-272">[Документация по Apache Kafka](http://kafka.apache.org/documentation.html) на сайте kafka.apache.org</span><span class="sxs-lookup"><span data-stu-id="f790f-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="f790f-273">Используйте MirrorMaker toocreate реплику Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f790f-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="f790f-274">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f790f-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="f790f-275">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f790f-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="f790f-276">Подключение через виртуальную сеть Azure tooKafka</span><span class="sxs-lookup"><span data-stu-id="f790f-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
