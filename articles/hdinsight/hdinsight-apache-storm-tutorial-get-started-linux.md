---
title: "Примеры начального уровня aaaStorm Apache Storm на HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toodo анализа больших данных и обработки данных в режиме реального времени с помощью Apache Storm и hello примеры начального уровня storm на HDInsight."
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
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="771c3-104">Приступая к работе с Apache Storm на HDInsight с помощью примеров storm начального приветствия</span><span class="sxs-lookup"><span data-stu-id="771c3-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="771c3-105">Узнайте, как toouse Apache Storm в HDInsight с помощью hello примеры начального уровня storm.</span><span class="sxs-lookup"><span data-stu-id="771c3-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="771c3-106">Apache Storm — это масштабируемая отказоустойчивая распределенная система выполнения расчетов для обработки данных потоковой передачи в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="771c3-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="771c3-107">С помощью Storm вы можете создать в Azure HDInsight облачный кластер, который анализирует данные в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="771c3-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="771c3-108">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="771c3-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="771c3-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="771c3-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="771c3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="771c3-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="771c3-111">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="771c3-111">**An Azure subscription**.</span></span> <span data-ttu-id="771c3-112">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="771c3-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="771c3-113">**Знакомство с SSH и SCP**.</span><span class="sxs-lookup"><span data-stu-id="771c3-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="771c3-114">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="771c3-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="771c3-115">Создание кластера Storm</span><span class="sxs-lookup"><span data-stu-id="771c3-115">Create a Storm cluster</span></span>

<span data-ttu-id="771c3-116">Используйте следующие шаги toocreate Storm в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="771c3-117">Из hello [портал Azure](https://portal.azure.com)выберите **+ создать**, **аналитики + аналитика**, а затем выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="771c3-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Создание кластера HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="771c3-119">Из hello **основы** колонке введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="771c3-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="771c3-120">**Имя кластера**: hello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="771c3-121">**Подписки**: выберите toouse hello подписки.</span><span class="sxs-lookup"><span data-stu-id="771c3-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="771c3-122">**Кластер пользователя для входа** и **входа пароль кластера**: hello входа при доступе к hello кластера по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="771c3-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="771c3-123">Можно использовать эти учетные данные tooaccess службы как hello Ambari веб-интерфейса или REST API.</span><span class="sxs-lookup"><span data-stu-id="771c3-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="771c3-124">**Secure Shell (SSH) username**: hello имя входа, используемое при доступе к hello кластера через SSH.</span><span class="sxs-lookup"><span data-stu-id="771c3-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="771c3-125">По умолчанию hello пароль является hello то же, что пароль имени входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="771c3-126">**Группа ресурсов**: hello ресурсов группы toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="771c3-127">**Расположение**: hello регион Azure toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Выберите подписку.](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="771c3-129">Выберите **кластера типа**, а затем набор hello Далее значения hello **конфигурации кластера** колонки:</span><span class="sxs-lookup"><span data-stu-id="771c3-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="771c3-130">**Тип кластера**: Storm.</span><span class="sxs-lookup"><span data-stu-id="771c3-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="771c3-131">**Операционная система**: Linux.</span><span class="sxs-lookup"><span data-stu-id="771c3-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="771c3-132">**Версия**: Storm 1.1.0 (HDI 3.6).</span><span class="sxs-lookup"><span data-stu-id="771c3-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="771c3-133">**Ценовая категория кластера**: "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="771c3-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="771c3-134">Наконец, используйте hello **выберите** кнопку toosave параметры.</span><span class="sxs-lookup"><span data-stu-id="771c3-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Выбор типа кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="771c3-136">После выбора типа hello кластера использовать hello __выберите__ tooset hello кластера тип кнопки.</span><span class="sxs-lookup"><span data-stu-id="771c3-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="771c3-137">Затем используйте hello __Далее__ кнопку toofinish базовой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="771c3-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="771c3-138">Из hello **хранения** колонке выберите или создайте учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="771c3-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="771c3-139">Hello в данном пошаговом руководстве оставьте hello другие поля в этой колонке в значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="771c3-140">Используйте hello __Далее__ кнопку toosave хранилища конфигурации.</span><span class="sxs-lookup"><span data-stu-id="771c3-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Задайте параметры учетной записи хранилища hello для HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="771c3-142">Из hello **Сводка** колонке проверить настройку hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="771c3-143">Используйте hello __изменить__ связывает toochange все параметры, которые являются неправильными.</span><span class="sxs-lookup"><span data-stu-id="771c3-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="771c3-144">Наконец используйте the__Create__ кнопку toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Сводка по конфигурации кластера](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="771c3-146">Он может занять too20 минут toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="771c3-147">Запуск примера storm-starter в HDInsight</span><span class="sxs-lookup"><span data-stu-id="771c3-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="771c3-148">Подключите кластер HDInsight toohello с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="771c3-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="771c3-149">Если вы использовали toosecure пароль учетной записи пользователя SSH, не запрошенные tooenter его.</span><span class="sxs-lookup"><span data-stu-id="771c3-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="771c3-150">Если используется открытый ключ, необходимо с помощью hello `-i` toospecify параметр hello соответствующим закрытым ключом.</span><span class="sxs-lookup"><span data-stu-id="771c3-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="771c3-151">Например, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="771c3-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="771c3-152">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="771c3-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="771c3-153">Используйте следующие команды toostart пример топологии hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="771c3-154">В предыдущих версиях HDInsight, имя класса hello hello топологии — `storm.starter.WordCountTopology` вместо `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="771c3-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="771c3-155">Эта команда запускает hello пример счетчика слов топологии на кластере hello, понятное имя «wordcount».</span><span class="sxs-lookup"><span data-stu-id="771c3-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="771c3-156">Случайным образом формирует предложения и число hello вхождения каждого слова в предложениях hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="771c3-157">При отправке кластеру toohello топологии, прежде всего необходимо скопировать файл hello JAR-файл, содержащий hello кластера перед использованием hello `storm` команды.</span><span class="sxs-lookup"><span data-stu-id="771c3-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="771c3-158">Используйте hello `scp` hello toocopy командный файл.</span><span class="sxs-lookup"><span data-stu-id="771c3-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="771c3-159">Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="771c3-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="771c3-160">Пример счетчика слов Hello и другие примеры начального уровня storm уже включены в кластере в `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="771c3-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="771c3-161">Если вы заинтересованы в просмотре источника hello примеры начального уровня storm hello, можно найти код hello в [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="771c3-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="771c3-162">Это ссылка для версии Storm 1.1.x, поставляемая вместе с HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="771c3-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="771c3-163">Для других версий Storm использовать hello __ветви__ кнопку вверху hello tooselect страницы приветствия на другую версию Storm.</span><span class="sxs-lookup"><span data-stu-id="771c3-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="771c3-164">Монитор hello топологии</span><span class="sxs-lookup"><span data-stu-id="771c3-164">Monitor hello topology</span></span>

<span data-ttu-id="771c3-165">Hello Storm пользовательского интерфейса предоставляет веб-интерфейс для работы с управлением топологии и включены в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="771c3-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="771c3-166">Используйте следующие шаги toomonitor hello топологии с помощью пользовательского интерфейса Storm hello hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="771c3-167">hello toodisplay Storm пользовательского интерфейса, откройте браузер web toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="771c3-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="771c3-168">Замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="771c3-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="771c3-169">При получении запроса tooprovide имя пользователя и пароль, введите Здравствуйте, администратор кластера (администратор) и пароль, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="771c3-170">В разделе **топологии Сводка**выберите hello **wordcount** запись в hello **имя** столбца.</span><span class="sxs-lookup"><span data-stu-id="771c3-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="771c3-171">Отображается информация о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-171">Information about hello topology is displayed.</span></span>

    ![Панель мониторинга Storm со сведениями о топологии WordCount в storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="771c3-173">На этой странице представлены hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="771c3-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="771c3-174">**Топология stats** -основные сведения о производительности топологии hello, организованных в времени windows.</span><span class="sxs-lookup"><span data-stu-id="771c3-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="771c3-175">Выбор временного hello определенное время окна изменения окна для сведений, отображаемых в других разделах страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="771c3-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="771c3-176">**Spouts** -основные сведения о spouts, включая hello последней ошибки, возвращенный каждого spout.</span><span class="sxs-lookup"><span data-stu-id="771c3-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="771c3-177">**Bolts** (Сита) — основная информация о ситах.</span><span class="sxs-lookup"><span data-stu-id="771c3-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="771c3-178">**Конфигурация топологии** -подробные сведения о настройке топологии hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="771c3-179">Этой странице также содержатся действия, которые могут быть выполнены на hello топологии:</span><span class="sxs-lookup"><span data-stu-id="771c3-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="771c3-180">**Activate** (Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="771c3-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="771c3-181">**Deactivate** (Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="771c3-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="771c3-182">**Перебалансировка** -корректирует параллелизм hello hello топологии.</span><span class="sxs-lookup"><span data-stu-id="771c3-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="771c3-183">После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии.</span><span class="sxs-lookup"><span data-stu-id="771c3-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="771c3-184">Перераспределения корректирует параллелизм toocompensate для hello увеличить или уменьшить количество узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="771c3-185">Дополнительные сведения см. в разделе [основные сведения о топологии Storm параллелизма hello](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="771c3-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="771c3-186">**KILL** -завершает топологии Storm после hello указано время ожидания.</span><span class="sxs-lookup"><span data-stu-id="771c3-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="771c3-187">На этой странице выберите запись из hello **Spouts** или **болтов** раздела.</span><span class="sxs-lookup"><span data-stu-id="771c3-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="771c3-188">Отображается информация о hello выбранного компонента.</span><span class="sxs-lookup"><span data-stu-id="771c3-188">Information about hello selected component is displayed.</span></span>

    ![Панель мониторинга Storm со сведениями о выбранных компонентах.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="771c3-190">На этой странице отображаются hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="771c3-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="771c3-191">**Spout/молнии stats** -основные сведения о производительности компонента hello, организованных в времени windows.</span><span class="sxs-lookup"><span data-stu-id="771c3-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="771c3-192">Выбор временного hello определенное время окна изменения окна для сведений, отображаемых в других разделах страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="771c3-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="771c3-193">**Статистика ввода** (только винта) - сведения о компонентах, которые создают данные, используемые молнии hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="771c3-194">**Output stats** (Статистика вывода) — информация о данных, созданных этим ситом.</span><span class="sxs-lookup"><span data-stu-id="771c3-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="771c3-195">**Executors** (Исполнители) — информация об экземплярах этого компонента.</span><span class="sxs-lookup"><span data-stu-id="771c3-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="771c3-196">**Errors** (Ошибки) — ошибки, созданные этим компонентом.</span><span class="sxs-lookup"><span data-stu-id="771c3-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="771c3-197">При просмотре сведений hello spout или молнии, выберите ее из hello **порт** столбца в hello **исполнителей** статьи tooview сведения для конкретного экземпляра компонента hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="771c3-198">В этом примере hello word **семь** произошла 1493957 раз.</span><span class="sxs-lookup"><span data-stu-id="771c3-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="771c3-199">Этот счетчик представляет, сколько раз с момента запуска этой топологии произошла слово hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="771c3-200">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="771c3-200">Stop hello topology</span></span>

<span data-ttu-id="771c3-201">Вернуть toohello **топологии Сводка** страницы для топологии hello количество слов, а затем выберите hello **Kill** кнопку hello **действия топологии** раздела.</span><span class="sxs-lookup"><span data-stu-id="771c3-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="771c3-202">При появлении запроса введите значение 10 для hello toowait секунд перед остановкой hello топологии.</span><span class="sxs-lookup"><span data-stu-id="771c3-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="771c3-203">По истечении периода ожидания hello топологии hello больше не отображается при посещении hello **Storm пользовательского интерфейса** hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="771c3-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="771c3-204">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="771c3-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="771c3-205">Если при создании кластеров HDInsight возникли проблемы, просмотрите раздел [Access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) (Требования к контролю доступа).</span><span class="sxs-lookup"><span data-stu-id="771c3-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="771c3-206"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="771c3-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="771c3-207">В этом учебнике Apache Storm вы узнали основы работы с Storm на HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="771c3-208">Далее, узнайте, как слишком[на языке Java, разработка топологии с помощью Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="771c3-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="771c3-209">Если вы уже знакомы с разработке на языке Java топологии и toodeploy существующие tooHDInsight топологии, см. раздел [развертывание и управление ими Apache Storm топологии на HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="771c3-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="771c3-210">Если вы разработчик .NET, вы можете создать топологию C# или гибридную топологию C# или Java с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="771c3-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="771c3-211">Дополнительные сведения см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="771c3-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="771c3-212">Примеры топологий, которые могут использоваться с Storm на HDInsight см. следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="771c3-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="771c3-213">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="771c3-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
