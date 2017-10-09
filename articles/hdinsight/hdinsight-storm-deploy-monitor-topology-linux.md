---
title: "aaaDeploy и управления ими Apache Storm топологии на основе Linux HDInsight | Документы Microsoft"
description: "Узнайте, как toodeploy, мониторинг и управление ими с помощью hello Storm панели мониторинга на основе Linux HDInsight топологии Apache Storm. Использование инструментов Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="ec006-104">Развертывание топологий Apache Storm в HDInsight и управление ими</span><span class="sxs-lookup"><span data-stu-id="ec006-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="ec006-105">В этом документе основы hello управление и мониторинг топологии Storm, работающие на ураган в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec006-106">Hello шаги в этой статье, требуют Storm на основе Linux в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="ec006-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ec006-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ec006-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ec006-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="ec006-109">Сведения о развертывании и мониторинге топологий в HDInsight под управлением Windows см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ec006-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec006-110">Prerequisites</span></span>

* <span data-ttu-id="ec006-111">**Storm под управлением Linux в кластере HDInsight.** Инструкции по созданию кластера см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="ec006-112">(Необязательно.) **Знакомство с SSH и SCP**. Дополнительные сведения см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="ec006-113">(Необязательно) **Visual Studio**: пакет SDK Azure 2.5.1 или более поздней версии и hello Озера Data Tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec006-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="ec006-114">Дополнительные сведения см. в статье [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="ec006-115">Одно из следующих версий Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="ec006-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="ec006-116">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="ec006-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="ec006-117">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="ec006-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="ec006-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ec006-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="ec006-119">Visual Studio 2015 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="ec006-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="ec006-120">Visual Studio 2017 (любой выпуск).</span><span class="sxs-lookup"><span data-stu-id="ec006-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="ec006-121">В рамках hello рабочей нагрузки Azure установлены средства Озера данных для Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ec006-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="ec006-122">Отправка топологии: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec006-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="ec006-123">Средства HDInsight Hello может быть используется toosubmit C# или гибридной топологии tooyour Storm кластера.</span><span class="sxs-lookup"><span data-stu-id="ec006-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="ec006-124">следующие шаги Hello используйте образец приложения.</span><span class="sxs-lookup"><span data-stu-id="ec006-124">hello following steps use a sample application.</span></span> <span data-ttu-id="ec006-125">Сведения о создании собственных топологий с помощью средства HDInsight hello см. в разделе [топологии разработки C# с помощью hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="ec006-126">Если вы еще не установили hello последнюю версию средств hello Озера данных для Visual Studio, в разделе [приступить к работе с помощью средств Озера данных для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec006-127">Hello средства Озера данных для Visual Studio ранее назывались hello средства HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec006-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="ec006-128">Средства Озера данных для Visual Studio включены в hello __рабочей нагрузки Azure__ для Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ec006-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="ec006-129">Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="ec006-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="ec006-130">В hello **новый проект** диалогового окна разверните **установленные** > **шаблоны**, а затем выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ec006-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="ec006-131">Выберите из списка шаблонов hello **Storm пример**.</span><span class="sxs-lookup"><span data-stu-id="ec006-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="ec006-132">Внизу hello диалогового окна «hello» введите имя для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="ec006-134">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ec006-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ec006-135">Если необходимо, введите учетные данные входа hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ec006-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="ec006-136">При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="ec006-137">Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="ec006-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="ec006-138">Можно отслеживать факт отправки hello выполнена с помощью hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="ec006-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="ec006-139">Отправить топологии: SSH и hello Storm команды</span><span class="sxs-lookup"><span data-stu-id="ec006-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="ec006-140">Используйте кластер HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="ec006-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="ec006-141">Замените **USERNAME** hello имя входа SSH.</span><span class="sxs-lookup"><span data-stu-id="ec006-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="ec006-142">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="ec006-143">Дополнительные сведения об использовании SSH tooconnect tooyour HDInsight кластера см. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ec006-144">Используйте следующие команды toostart пример топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="ec006-145">Эта команда запускает hello пример счетчика слов топологии на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="ec006-146">В этой топологии случайным образом создавать предложения и число hello вхождения каждого слова в предложениях hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ec006-147">При отправке кластера toohello топологии, прежде всего необходимо скопировать файл hello JAR-файл, содержащий hello кластера перед использованием hello `storm` команды.</span><span class="sxs-lookup"><span data-stu-id="ec006-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="ec006-148">toocopy hello toohello файлового, можно использовать hello `scp` команды.</span><span class="sxs-lookup"><span data-stu-id="ec006-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="ec006-149">Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="ec006-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="ec006-150">Пример счетчика слов Hello и другие примеры начального уровня storm уже включены в кластере в `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="ec006-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="ec006-151">Отправка топологии: программный метод</span><span class="sxs-lookup"><span data-stu-id="ec006-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="ec006-152">Программным путем можно развернуть tooStorm топологии на HDInsight путем взаимодействия с hello Nimbus службу, размещенную в кластере.</span><span class="sxs-lookup"><span data-stu-id="ec006-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="ec006-153">[https://github.com/Azure-Samples/hdinsight-Java-deploy-storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) содержит пример приложения Java, демонстрирующий, как toodeploy и запуска топологии через hello Nimbus службы.</span><span class="sxs-lookup"><span data-stu-id="ec006-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="ec006-154">Мониторинг и управление: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec006-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="ec006-155">Здравствуйте, когда топологии успешно отправлена с помощью Visual Studio, **Storm топологии** просмотра отобразится hello кластера.</span><span class="sxs-lookup"><span data-stu-id="ec006-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="ec006-156">Выберите топологию hello hello список tooview сведения о hello под управлением топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="ec006-158">Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="ec006-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="ec006-159">Выберите фигуру hello для hello spouts или болтов tooview сведения об этих компонентах.</span><span class="sxs-lookup"><span data-stu-id="ec006-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="ec006-160">Для каждого выбранного элемента открывается новое окно.</span><span class="sxs-lookup"><span data-stu-id="ec006-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="ec006-161">Деактивация и повторная активация</span><span class="sxs-lookup"><span data-stu-id="ec006-161">Deactivate and reactivate</span></span>

<span data-ttu-id="ec006-162">Деактивация топологии приостанавливает ее до завершения или повторной активации.</span><span class="sxs-lookup"><span data-stu-id="ec006-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="ec006-163">tooperform в этих операциях используется hello __деактивировать__ и __повторно активировать__ кнопки вверху hello hello __топологии Сводка__.</span><span class="sxs-lookup"><span data-stu-id="ec006-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="ec006-164">Повторная балансировка</span><span class="sxs-lookup"><span data-stu-id="ec006-164">Rebalance</span></span>

<span data-ttu-id="ec006-165">Перераспределения топологии позволяет hello системы toorevise hello параллелизма hello топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="ec006-166">Например если изменения размера кластера tooadd hello дополнительные заметки, перераспределения позволяет топологии toosee hello новых узлов.</span><span class="sxs-lookup"><span data-stu-id="ec006-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="ec006-167">toorebalance топологии, используйте hello __Перебалансировка__ кнопку вверху hello hello __топологии Сводка__.</span><span class="sxs-lookup"><span data-stu-id="ec006-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="ec006-168">Сначала перераспределения топологии деактивирует топология hello, затем равномерно перераспределяет работников в кластере hello, а затем наконец возвращает состояние toohello топологии hello, которое было до возникновения перераспределения.</span><span class="sxs-lookup"><span data-stu-id="ec006-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="ec006-169">Поэтому если топологии hello был активен, он снова становится активным.</span><span class="sxs-lookup"><span data-stu-id="ec006-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="ec006-170">Если она была отключена, то останется таковой.</span><span class="sxs-lookup"><span data-stu-id="ec006-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="ec006-171">Завершение работы топологии</span><span class="sxs-lookup"><span data-stu-id="ec006-171">Kill a topology</span></span>

<span data-ttu-id="ec006-172">Топологии storm продолжения, пока они не будут остановлены или hello кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="ec006-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="ec006-173">toostop топологии, используйте hello __Kill__ кнопку вверху hello hello __топологии Сводка__.</span><span class="sxs-lookup"><span data-stu-id="ec006-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="ec006-174">Мониторинг и управление: SSH и hello Storm команды</span><span class="sxs-lookup"><span data-stu-id="ec006-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="ec006-175">Hello `storm` программа позволяет toowork с работающими топологии из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="ec006-176">Чтобы вывести полный список команд, воспользуйтесь `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="ec006-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="ec006-177">Вывод списка топологий</span><span class="sxs-lookup"><span data-stu-id="ec006-177">List topologies</span></span>

<span data-ttu-id="ec006-178">Используйте hello, следующая команда toolist всех запущенных топологии:</span><span class="sxs-lookup"><span data-stu-id="ec006-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="ec006-179">Эта команда возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="ec006-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="ec006-180">Деактивация и повторная активация</span><span class="sxs-lookup"><span data-stu-id="ec006-180">Deactivate and reactivate</span></span>

<span data-ttu-id="ec006-181">Деактивация топологии приостанавливает ее до завершения или повторной активации.</span><span class="sxs-lookup"><span data-stu-id="ec006-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="ec006-182">Используйте следующие команды toodeactivate hello и повторной активации:</span><span class="sxs-lookup"><span data-stu-id="ec006-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="ec006-183">Завершение запущенной топологии</span><span class="sxs-lookup"><span data-stu-id="ec006-183">Kill a running topology</span></span>

<span data-ttu-id="ec006-184">Топологии Storm после запуска продолжают работать до тех пор, пока не будут остановлены.</span><span class="sxs-lookup"><span data-stu-id="ec006-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="ec006-185">toostop топологии hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ec006-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="ec006-186">Повторная балансировка</span><span class="sxs-lookup"><span data-stu-id="ec006-186">Rebalance</span></span>

<span data-ttu-id="ec006-187">Перераспределения топологии позволяет hello системы toorevise hello параллелизма hello топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="ec006-188">Например если изменения размера кластера tooadd hello дополнительные заметки, перераспределения позволяет топологии toosee hello новых узлов.</span><span class="sxs-lookup"><span data-stu-id="ec006-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="ec006-189">Сначала перераспределения топологии деактивирует топология hello, затем равномерно перераспределяет работников в кластере hello, а затем наконец возвращает состояние toohello топологии hello, которое было до возникновения перераспределения.</span><span class="sxs-lookup"><span data-stu-id="ec006-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="ec006-190">Поэтому если топологии hello был активен, он снова становится активным.</span><span class="sxs-lookup"><span data-stu-id="ec006-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="ec006-191">Если она была отключена, то останется таковой.</span><span class="sxs-lookup"><span data-stu-id="ec006-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="ec006-192">Мониторинг и управление: пользовательский интерфейс Storm</span><span class="sxs-lookup"><span data-stu-id="ec006-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="ec006-193">Hello Storm пользовательского интерфейса предоставляет веб-интерфейс для работы с управлением топологии и включены в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="ec006-194">hello tooview Storm пользовательского интерфейса, используйте браузер web tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, где **CLUSTERNAME** — hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="ec006-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ec006-195">При получении запроса tooprovide имя пользователя и пароль, введите Здравствуйте, администратор кластера (администратор) и пароль, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="ec006-196">Главная страница</span><span class="sxs-lookup"><span data-stu-id="ec006-196">Main page</span></span>

<span data-ttu-id="ec006-197">Главная страница Hello hello Storm пользовательского интерфейса предоставляет hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ec006-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="ec006-198">**Сводка кластера**: основные сведения о кластере Storm hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="ec006-199">**Topology summary**(Сводка по топологиям) — список запущенных топологий.</span><span class="sxs-lookup"><span data-stu-id="ec006-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="ec006-200">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="ec006-201">**Допуск сводки**: сведения о начальника Storm hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="ec006-202">**Конфигурация nimbus**: Nimbus конфигурации для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="ec006-203">Topology summary</span><span class="sxs-lookup"><span data-stu-id="ec006-203">Topology summary</span></span>

<span data-ttu-id="ec006-204">При выборе ссылки из hello **топологии Сводка** разделе отображаются следующие сведения о топологии hello hello:</span><span class="sxs-lookup"><span data-stu-id="ec006-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="ec006-205">**Сводка топологии**: основные сведения о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="ec006-206">**Топология действия**: операции управления, которые можно выполнять для топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="ec006-207">**Activate**(Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="ec006-208">**Deactivate**(Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="ec006-209">**Перебалансировка**: корректирует параллелизм hello hello топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="ec006-210">После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="ec006-211">Эта операция позволяет toocompensate hello топологии tooadjust параллелизма для hello увеличивается или уменьшается число узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="ec006-212">Дополнительные сведения см. в разделе <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">основные сведения о топологии Storm параллелизма hello</a>.</span><span class="sxs-lookup"><span data-stu-id="ec006-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="ec006-213">**KILL**: завершает топологии Storm после hello указано время ожидания.</span><span class="sxs-lookup"><span data-stu-id="ec006-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="ec006-214">**Топология stats**: статистические данные о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="ec006-215">tooset Здравствуйте период времени для оставшихся записей на странице приветствия hello, используйте ссылки hello в hello **окна** столбца.</span><span class="sxs-lookup"><span data-stu-id="ec006-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="ec006-216">**Spouts**: hello spouts используемой топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="ec006-217">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных spouts.</span><span class="sxs-lookup"><span data-stu-id="ec006-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="ec006-218">**Болтов**: hello винты используемой топологии hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="ec006-219">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных винты.</span><span class="sxs-lookup"><span data-stu-id="ec006-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="ec006-220">**Конфигурация топологии**: hello конфигурации hello выбранной топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="ec006-221">Сводка по воронкам и ситам</span><span class="sxs-lookup"><span data-stu-id="ec006-221">Spout and Bolt summary</span></span>

<span data-ttu-id="ec006-222">Выбрав spout hello **Spouts** или **болтов** разделы отображает hello следующую информацию о hello выбранного элемента:</span><span class="sxs-lookup"><span data-stu-id="ec006-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="ec006-223">**Сводка компонентов**: основные сведения о hello spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="ec006-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="ec006-224">**Spout/молнии stats**: статистику hello spout или винта.</span><span class="sxs-lookup"><span data-stu-id="ec006-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="ec006-225">tooset Здравствуйте период времени для оставшихся записей на странице приветствия hello, используйте ссылки hello в hello **окна** столбца.</span><span class="sxs-lookup"><span data-stu-id="ec006-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="ec006-226">**Статистика ввода** (только винта): сведения о hello входные потоки, используемые hello молнии.</span><span class="sxs-lookup"><span data-stu-id="ec006-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="ec006-227">**Выходные данные статистики**: сведения о потоках hello, генерируемой это spout или винта.</span><span class="sxs-lookup"><span data-stu-id="ec006-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="ec006-228">**Исполнители**: сведения об экземплярах hello hello spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="ec006-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="ec006-229">Выберите hello **порт** запись для tooview определенного исполнителя, создается журнал диагностических сведений для данного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="ec006-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="ec006-230">**Errors**(Ошибки) — информация об ошибках для данной воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="ec006-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="ec006-231">Мониторинг и управление: REST API</span><span class="sxs-lookup"><span data-stu-id="ec006-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="ec006-232">Hello пользовательского интерфейса Storm построено на основе hello REST API, чтобы выполнить аналогичные отслеживание и управление ими функциональные возможности с помощью API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="ec006-233">Hello API-интерфейса REST toocreate пользовательские средства можно использовать для управления и мониторинга Storm топологии.</span><span class="sxs-lookup"><span data-stu-id="ec006-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="ec006-234">Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="ec006-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="ec006-235">Hello следующие сведения являются hello конкретных toousing API REST с Apache Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec006-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec006-236">Hello Storm REST API не является общедоступным более hello Интернета и должны быть доступны с помощью SSH туннеля toohello HDInsight головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="ec006-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="ec006-237">Сведения о создании и использовании туннель SSH см. в разделе [использование SSH туннелирование tooaccess Ambari веб-интерфейса пользователя, диспетчер ресурсов, JobHistory, NameNode, Oozie и других сетевых интерфейсов](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="ec006-238">Базовый универсальный код ресурса</span><span class="sxs-lookup"><span data-stu-id="ec006-238">Base URI</span></span>

<span data-ttu-id="ec006-239">Hello базовый URI для hello REST API в кластерах HDInsight под управлением Linux доступна на головном узле hello в **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="ec006-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="ec006-240">имя домена Hello hello головного узла создается во время создания кластера и не является статическим.</span><span class="sxs-lookup"><span data-stu-id="ec006-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="ec006-241">Можно найти hello полное доменное имя (FQDN) для головного узла кластера hello несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="ec006-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="ec006-242">**Из сеанса SSH**: команда hello `headnode -f` из кластера toohello сеансу SSH.</span><span class="sxs-lookup"><span data-stu-id="ec006-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="ec006-243">**Из веб-Ambari**: выберите **службы** hello вверху страницы приветствия, а затем нажмите **Storm**.</span><span class="sxs-lookup"><span data-stu-id="ec006-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="ec006-244">Из hello **Сводка** выберите **Storm пользовательского интерфейса сервера**.</span><span class="sxs-lookup"><span data-stu-id="ec006-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="ec006-245">Hello полное доменное имя узла hello, на котором выполняется hello Storm пользовательского интерфейса и API-интерфейса REST является вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="ec006-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="ec006-246">**Из интерфейса API REST Ambari**: команда hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` ОС tooretrieve сведения об узле hello, hello Storm пользовательского интерфейса и интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="ec006-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="ec006-247">Замените **пароль** с hello пароль администратора для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="ec006-248">Замените **CLUSTERNAME** с именем кластера hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="ec006-249">В ответ hello запись hello «host_name» содержит hello полное доменное имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="ec006-250">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="ec006-250">Authentication</span></span>

<span data-ttu-id="ec006-251">Toohello запросы, необходимо использовать API-Интерфейс REST **обычной проверки подлинности**, поэтому использовать hello HDInsight кластер имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="ec006-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="ec006-252">Поскольку обычная проверка подлинности передается с помощью открытого текста, следует **всегда** использовать кластере hello toosecure подключений по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ec006-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="ec006-253">Возвращаемые значения</span><span class="sxs-lookup"><span data-stu-id="ec006-253">Return values</span></span>

<span data-ttu-id="ec006-254">Сведения, возвращаемые из hello API-интерфейса REST только может быть одновременно доступен из кода внутри кластера hello или виртуальных машин на hello одной виртуальной сети Azure как кластер hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="ec006-255">Например hello полное доменное имя (FQDN), возвращаемые для серверов Zookeeper недоступна из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ec006-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec006-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec006-256">Next Steps</span></span>

<span data-ttu-id="ec006-257">Теперь, когда вы узнали, как монитор и toodeploy топологии с помощью hello Storm панели мониторинга, узнайте, каким образом слишком[на языке Java, разработка топологии с помощью Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="ec006-258">Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ec006-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
