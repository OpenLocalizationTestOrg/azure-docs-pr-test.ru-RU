---
title: "Примеры storm-starter для работы с Apache Storm в HDInsight — Azure | Документация Майкрософт"
description: "Узнайте, как выполнять аналитику больших данных и обрабатывать информацию в режиме реального времени, используя Apache Storm и примеры storm-starter в HDInsight."
keywords: "storm-starter, пример apache storm"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="4e926-104">Начало работы с Apache Storm в HDInsight с использованием примеров storm-starter</span><span class="sxs-lookup"><span data-stu-id="4e926-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="4e926-105">Сведения о работе с Apache Storm в HDInsight с использованием примеров storm-starter.</span><span class="sxs-lookup"><span data-stu-id="4e926-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="4e926-106">Apache Storm — это масштабируемая отказоустойчивая распределенная система выполнения расчетов для обработки данных потоковой передачи в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="4e926-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="4e926-107">С помощью Storm вы можете создать в Azure HDInsight облачный кластер, который анализирует данные в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="4e926-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e926-108">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4e926-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4e926-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4e926-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e926-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4e926-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="4e926-111">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="4e926-111">**An Azure subscription**.</span></span> <span data-ttu-id="4e926-112">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4e926-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="4e926-113">**Знакомство с SSH и SCP**.</span><span class="sxs-lookup"><span data-stu-id="4e926-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="4e926-114">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4e926-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="4e926-115">Создание кластера Storm</span><span class="sxs-lookup"><span data-stu-id="4e926-115">Create a Storm cluster</span></span>

<span data-ttu-id="4e926-116">Чтобы создать Storm в кластере HDInsight, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4e926-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="4e926-117">На [портале Azure](https://portal.azure.com) последовательно выберите элементы **+Создать**, **Аналитика** и **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4e926-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Создание кластера HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="4e926-119">В колонке **Основные сведения** задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="4e926-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="4e926-120">**Имя кластера.** Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e926-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="4e926-121">**Подписка.** Выберите нужную подписку.</span><span class="sxs-lookup"><span data-stu-id="4e926-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="4e926-122">**Имя пользователя для входа в кластер** и **Пароль для входа в кластер**. Имя для входа в кластер по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4e926-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="4e926-123">Эти учетные данные используются для доступа к таким службам, как веб-интерфейс Ambari или REST API.</span><span class="sxs-lookup"><span data-stu-id="4e926-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="4e926-124">**Secure Shell (SSH) username** (Имя пользователя Secure Shell (SSH)). Имя для доступа к кластеру по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="4e926-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="4e926-125">По умолчанию пароль совпадает с паролем для входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="4e926-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="4e926-126">**Группа ресурсов.** Группа ресурсов, в которой будет создан кластер.</span><span class="sxs-lookup"><span data-stu-id="4e926-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="4e926-127">**Расположение.** Регион Azure, в котором будет создан кластер.</span><span class="sxs-lookup"><span data-stu-id="4e926-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![Выберите подписку.](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="4e926-129">Выберите **тип кластера** и в колонке **Конфигурация кластера** задайте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="4e926-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="4e926-130">**Тип кластера**: Storm.</span><span class="sxs-lookup"><span data-stu-id="4e926-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="4e926-131">**Операционная система**: Linux.</span><span class="sxs-lookup"><span data-stu-id="4e926-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="4e926-132">**Версия**: Storm 1.1.0 (HDI 3.6).</span><span class="sxs-lookup"><span data-stu-id="4e926-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="4e926-133">**Ценовая категория кластера**: "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="4e926-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="4e926-134">Затем нажмите кнопку **Выбрать**, чтобы сохранить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="4e926-134">Finally, use the **Select** button to save settings.</span></span>

    ![Выбор типа кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="4e926-136">Выбрав тип кластера, нажмите кнопку __Выбрать__, чтобы установить выбранный тип.</span><span class="sxs-lookup"><span data-stu-id="4e926-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="4e926-137">Затем нажмите кнопку __Далее__, чтобы завершить настройку основных параметров.</span><span class="sxs-lookup"><span data-stu-id="4e926-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="4e926-138">В колонке **Хранилище** выберите или создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4e926-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="4e926-139">Для действий, описанных в этом документе, в других полях этой колонки оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e926-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="4e926-140">Нажмите кнопку __Далее__, чтобы сохранить конфигурацию хранилища.</span><span class="sxs-lookup"><span data-stu-id="4e926-140">Use the __Next__ button to save storage configuration.</span></span>

    ![Настройка параметров учетной записи хранения для HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="4e926-142">В колонке **Сводка** просмотрите конфигурацию для кластера.</span><span class="sxs-lookup"><span data-stu-id="4e926-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="4e926-143">Используйте ссылки __Изменить__, чтобы изменить неправильные параметры.</span><span class="sxs-lookup"><span data-stu-id="4e926-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="4e926-144">Наконец, нажмите кнопку "Создать" для создания кластера.</span><span class="sxs-lookup"><span data-stu-id="4e926-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Сводка по конфигурации кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="4e926-146">Операция создания кластера может занять до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="4e926-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="4e926-147">Запуск примера storm-starter в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e926-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="4e926-148">Подключитесь к кластеру HDInsight с помощью протокола SSH:</span><span class="sxs-lookup"><span data-stu-id="4e926-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="4e926-149">Если для защиты учетной записи SSH используется пароль, то предлагается ввести его.</span><span class="sxs-lookup"><span data-stu-id="4e926-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="4e926-150">Если используется открытый ключ, то может потребоваться использовать параметр `-i`, чтобы указать соответствующий закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="4e926-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="4e926-151">Например, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="4e926-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="4e926-152">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4e926-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4e926-153">Запустите пример топологии, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4e926-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="4e926-154">В предыдущих версиях HDInsight использовалось имя класса топологии `storm.starter.WordCountTopology` вместо `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="4e926-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="4e926-155">Эта команда запускает в кластере пример топологии WordCount с понятным именем wordcount.</span><span class="sxs-lookup"><span data-stu-id="4e926-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="4e926-156">Он случайным образом формирует предложения и подсчитывает количество экземпляров каждого слова в предложениях.</span><span class="sxs-lookup"><span data-stu-id="4e926-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4e926-157">При отправке пользовательской топологии в кластер необходимо сначала скопировать JAR-файл, содержащий кластер, а затем воспользоваться командой `storm`.</span><span class="sxs-lookup"><span data-stu-id="4e926-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="4e926-158">Чтобы скопировать файл, воспользуйтесь командой `scp`.</span><span class="sxs-lookup"><span data-stu-id="4e926-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="4e926-159">Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="4e926-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="4e926-160">Пример WordCount и другие примеры storm-starter уже включены в ваш кластер в `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="4e926-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="4e926-161">Исходный код для примеров storm-starter можно найти здесь: [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="4e926-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="4e926-162">Это ссылка для версии Storm 1.1.x, поставляемая вместе с HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="4e926-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="4e926-163">Для других версий Storm нажмите кнопку __Ветвь__ в верхней части страницы и выберите нужную версию.</span><span class="sxs-lookup"><span data-stu-id="4e926-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="4e926-164">Мониторинг топологии</span><span class="sxs-lookup"><span data-stu-id="4e926-164">Monitor the topology</span></span>

<span data-ttu-id="4e926-165">Пользовательский интерфейс Storm предоставляет веб-интерфейс для работы с запущенными топологиями и включен в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e926-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="4e926-166">Чтобы начать мониторинг топологии из пользовательского интерфейса Storm, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4e926-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="4e926-167">Чтобы отобразить пользовательский интерфейс Storm, откройте в веб-браузере страницу с адресом https://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="4e926-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="4e926-168">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="4e926-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4e926-169">При появлении соответствующего запроса введите имя пользователя и пароль администратора кластера (admin), которые использовались при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="4e926-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="4e926-170">В разделе**Topology summary** (Сводка по топологии) выберите запись **wordcount** (количество слов) в столбце **Name** (Имя).</span><span class="sxs-lookup"><span data-stu-id="4e926-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="4e926-171">Отобразятся сведения о топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-171">Information about the topology is displayed.</span></span>

    ![Панель мониторинга Storm со сведениями о топологии WordCount в storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="4e926-173">Эта страница содержит следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="4e926-173">This page provides the following information:</span></span>

    * <span data-ttu-id="4e926-174">**Topology stats** (Статистика топологий) —основная информация о производительности топологии, упорядоченная по временным промежуткам.</span><span class="sxs-lookup"><span data-stu-id="4e926-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4e926-175">При выборе определенного временного промежутка меняется информация, отображаемая в других разделах страницы.</span><span class="sxs-lookup"><span data-stu-id="4e926-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="4e926-176">**Spouts** (Воронки) — основная информация о воронках, в том числе последняя ошибка, возвращенная каждой воронкой.</span><span class="sxs-lookup"><span data-stu-id="4e926-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="4e926-177">**Bolts** (Сита) — основная информация о ситах.</span><span class="sxs-lookup"><span data-stu-id="4e926-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="4e926-178">**Topology configuration** (Конфигурация топологии) — подробная информация о конфигурации топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="4e926-179">Эта страница также содержит действия, которые можно выполнять в топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="4e926-180">**Activate** (Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="4e926-181">**Deactivate** (Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="4e926-182">**Rebalance**(Повторная балансировка) — корректировка параллелизма топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="4e926-183">После изменения числа узлов в кластере необходимо выполнить повторную балансировку топологий.</span><span class="sxs-lookup"><span data-stu-id="4e926-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="4e926-184">Повторная балансировка корректирует параллелизм для компенсации увеличения или уменьшения количества узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="4e926-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="4e926-185">Дополнительные сведения см. в статье [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (Общие сведения о параллелизме топологии Storm).</span><span class="sxs-lookup"><span data-stu-id="4e926-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="4e926-186">**Kill** (Удалить) — останавливает выполнение топологии Storm по истечении заданного времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="4e926-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="4e926-187">На этой странице выберите запись и раздела **Spouts** (Воронки) или **Bolts** (Сита).</span><span class="sxs-lookup"><span data-stu-id="4e926-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="4e926-188">Отобразятся сведения о выбранном компоненте.</span><span class="sxs-lookup"><span data-stu-id="4e926-188">Information about the selected component is displayed.</span></span>

    ![Панель мониторинга Storm со сведениями о выбранных компонентах.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="4e926-190">На этой странице отображается следующая информация.</span><span class="sxs-lookup"><span data-stu-id="4e926-190">This page displays the following information:</span></span>

    * <span data-ttu-id="4e926-191">**Spout/Bolt stats** (Статистика воронки/сита) —основная информация о производительности соответствующего компонента, упорядоченная по временным промежуткам.</span><span class="sxs-lookup"><span data-stu-id="4e926-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4e926-192">При выборе определенного временного промежутка меняется информация, отображаемая в других разделах страницы.</span><span class="sxs-lookup"><span data-stu-id="4e926-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="4e926-193">**Input stats** (Статистика ввода, только для сита) — информация о компонентах, которые производят данные, используемые ситом.</span><span class="sxs-lookup"><span data-stu-id="4e926-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="4e926-194">**Output stats** (Статистика вывода) — информация о данных, созданных этим ситом.</span><span class="sxs-lookup"><span data-stu-id="4e926-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="4e926-195">**Executors** (Исполнители) — информация об экземплярах этого компонента.</span><span class="sxs-lookup"><span data-stu-id="4e926-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="4e926-196">**Errors** (Ошибки) — ошибки, созданные этим компонентом.</span><span class="sxs-lookup"><span data-stu-id="4e926-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="4e926-197">При просмотре информации о воронке и сите выберите запись из столбца **Port** (Порт) в разделе **Executors** (Исполнители), чтобы просмотреть информацию о конкретном экземпляре компонента.</span><span class="sxs-lookup"><span data-stu-id="4e926-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="4e926-198">В этом примере слово **seven** (семь) использовалось 1 493 957 раз.</span><span class="sxs-lookup"><span data-stu-id="4e926-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="4e926-199">Столько раз это слово было обнаружено с момента запуска данной топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="4e926-200">Остановка топологии</span><span class="sxs-lookup"><span data-stu-id="4e926-200">Stop the topology</span></span>

<span data-ttu-id="4e926-201">Вернитесь к странице **Topology summary** (Сводка по топологии), чтобы найти топологию подсчета слов, и нажмите кнопку **Kill** (Удалить) в разделе **Topology actions** (Действия топологии).</span><span class="sxs-lookup"><span data-stu-id="4e926-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="4e926-202">При появлении запроса введите 10 секунд ожидания перед остановкой топологии.</span><span class="sxs-lookup"><span data-stu-id="4e926-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="4e926-203">По истечении времени ожидания топология перестанет отображаться при переходе к разделу **Пользовательский интерфейс Storm** на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="4e926-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="4e926-204">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="4e926-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4e926-205">Если при создании кластеров HDInsight возникли проблемы, просмотрите раздел [Access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) (Требования к контролю доступа).</span><span class="sxs-lookup"><span data-stu-id="4e926-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="4e926-206"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e926-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="4e926-207">В этом руководстве по Apache Storm описаны основные принципы работы со Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e926-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="4e926-208">Затем вы можете научиться [разрабатывать топологии на платформе Java с помощью Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4e926-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="4e926-209">Если вы уже знакомы с разработкой топологий на основе Java и хотите развернуть существующую топологию в HDInsight, см. статью [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4e926-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="4e926-210">Если вы разработчик .NET, вы можете создать топологию C# или гибридную топологию C# или Java с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e926-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="4e926-211">Дополнительные сведения см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4e926-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="4e926-212">Например топологии, которые можно использовать при помощи Storm в HDInsight, см. в следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="4e926-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="4e926-213">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e926-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
