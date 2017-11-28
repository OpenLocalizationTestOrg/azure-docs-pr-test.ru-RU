---
title: "Развертывание топологий Apache Storm в HDInsight на основе Linux и управление ими | Документация Майкрософт"
description: "Узнайте, как развертывать и отслеживать топологии Apache Storm, а также управлять ими с помощью панели мониторинга Storm в HDInsight на основе Linux. Использование инструментов Hadoop для Visual Studio."
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="78f51-104">Развертывание топологий Apache Storm в HDInsight и управление ими</span><span class="sxs-lookup"><span data-stu-id="78f51-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="78f51-105">С помощью этого документа вы ознакомитесь с основами управления и мониторинга топологий Storm, работающих в Storm в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78f51-106">Для выполнения действий, описанных в этой статье, вам потребуется Storm под управлением Linux в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="78f51-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="78f51-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78f51-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="78f51-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="78f51-109">Сведения о развертывании и мониторинге топологий в HDInsight под управлением Windows см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="78f51-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78f51-110">Prerequisites</span></span>

* <span data-ttu-id="78f51-111">**Storm под управлением Linux в кластере HDInsight.** Инструкции по созданию кластера см. в статье [Руководство по Apache Storm в HDInsight: начало работы с анализом больших объемов данных в HDInsight с помощью примеров Storm Starter](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="78f51-112">(Необязательно.) **Знакомство с SSH и SCP**. Дополнительные сведения см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="78f51-113">(Необязательно.) **Visual Studio**. Пакет SDK для Azure 2.5.1 или более поздней версии и средства Azure Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78f51-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="78f51-114">Дополнительные сведения см. в статье [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="78f51-115">Одна из следующих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="78f51-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="78f51-116">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="78f51-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="78f51-117">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="78f51-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="78f51-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="78f51-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="78f51-119">Visual Studio 2015 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="78f51-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="78f51-120">Visual Studio 2017 (любой выпуск).</span><span class="sxs-lookup"><span data-stu-id="78f51-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="78f51-121">Средства Data Lake для Visual Studio 2017 устанавливаются как часть рабочей нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="78f51-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="78f51-122">Отправка топологии: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78f51-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="78f51-123">Средства HDInsight можно использовать для отправки топологии C# или гибридной топологии в кластер Storm.</span><span class="sxs-lookup"><span data-stu-id="78f51-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="78f51-124">Далее используется пример приложения.</span><span class="sxs-lookup"><span data-stu-id="78f51-124">The following steps use a sample application.</span></span> <span data-ttu-id="78f51-125">Информацию о создании собственных топологий с помощью средств HDInsight см. в разделе [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="78f51-126">Если вы еще не установили последнюю версию средств Data Lake для Visual Studio, прочитайте статью [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="78f51-127">Средства Data Lake для Visual Studio ранее назывались средствами HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78f51-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="78f51-128">Средства Data Lake для Visual Studio входят в состав __рабочей нагрузки Azure__ для Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="78f51-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="78f51-129">Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="78f51-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="78f51-130">В диалоговом окне **Новый проект** разверните **Установленные** > **Шаблоны** и выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="78f51-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="78f51-131">В списке шаблонов выберите **Пример Storm**.</span><span class="sxs-lookup"><span data-stu-id="78f51-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="78f51-132">В нижней части диалогового окна введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="78f51-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="78f51-134">В **обозревателе решений** щелкните правой кнопкой мыши проект и выберите **Submit to Storm on HDInsight** (Отправить в Storm в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="78f51-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78f51-135">При появлении запроса введите учетные данные входа для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="78f51-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="78f51-136">Если у вас несколько подписок, воспользуйтесь той, что содержит ваш кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="78f51-137">Выберите Storm в кластере HDInsight из раскрывающегося списка **Кластер Storm** и щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="78f51-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="78f51-138">Вы можете отслеживать выполнение отправки в окне **Выходные данные** .</span><span class="sxs-lookup"><span data-stu-id="78f51-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="78f51-139">Отправка топологии: SSH и команда Storm</span><span class="sxs-lookup"><span data-stu-id="78f51-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="78f51-140">Подключитесь к кластеру HDInsight с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="78f51-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="78f51-141">Замените **USERNAME** именем пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="78f51-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="78f51-142">Замените **CLUSTERNAME** именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="78f51-143">Дополнительные сведения об использовании SSH для подключения к кластеру HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="78f51-144">Запустите пример топологии, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="78f51-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="78f51-145">Эта команда запускает пример топологии WordCount в кластере.</span><span class="sxs-lookup"><span data-stu-id="78f51-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="78f51-146">Эта топология случайным образом формирует предложения и подсчитывает количество вхождений каждого слова в предложениях.</span><span class="sxs-lookup"><span data-stu-id="78f51-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="78f51-147">При отправке топологии в кластер необходимо сначала скопировать jar-файл, содержащий кластер, а затем воспользоваться командой `storm`.</span><span class="sxs-lookup"><span data-stu-id="78f51-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="78f51-148">Чтобы скопировать файл в кластер, можно использовать команду `scp`.</span><span class="sxs-lookup"><span data-stu-id="78f51-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="78f51-149">Например, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="78f51-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="78f51-150">Пример WordCount и другие начальные примеры использования Storm уже включены в ваш кластер в `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="78f51-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="78f51-151">Отправка топологии: программный метод</span><span class="sxs-lookup"><span data-stu-id="78f51-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="78f51-152">Вы можете программно развернуть топологию в Storm в HDInsight, обмениваясь данными со службой Nimbus, размещенной в кластере.</span><span class="sxs-lookup"><span data-stu-id="78f51-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="78f51-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) приведен пример приложения Java, в котором показано, как развернуть и запустить топологию с помощью службы Nimbus.</span><span class="sxs-lookup"><span data-stu-id="78f51-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="78f51-154">Мониторинг и управление: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78f51-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="78f51-155">После успешной отправки топологии с помощью Visual Studio отображается представление **Storm Topologies** (Топологии Storm) для кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="78f51-156">Выберите топологию в списке, чтобы просмотреть информацию о выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-156">Select the topology from the list to view information about the running topology.</span></span>

![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="78f51-158">Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="78f51-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="78f51-159">Выделите компонент spout или bolt, чтобы просмотреть информацию о нем.</span><span class="sxs-lookup"><span data-stu-id="78f51-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="78f51-160">Для каждого выбранного элемента открывается новое окно.</span><span class="sxs-lookup"><span data-stu-id="78f51-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="78f51-161">Деактивация и повторная активация</span><span class="sxs-lookup"><span data-stu-id="78f51-161">Deactivate and reactivate</span></span>

<span data-ttu-id="78f51-162">Деактивация топологии приостанавливает ее до завершения или повторной активации.</span><span class="sxs-lookup"><span data-stu-id="78f51-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="78f51-163">Для этих операций используйте кнопки __Отключить__ и __Активировать повторно__ в верхней части окна __Topology Summary__ (Сводка топологии).</span><span class="sxs-lookup"><span data-stu-id="78f51-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="78f51-164">Повторная балансировка</span><span class="sxs-lookup"><span data-stu-id="78f51-164">Rebalance</span></span>

<span data-ttu-id="78f51-165">Повторная балансировка топологии позволяет системе пересмотреть параллелизм топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="78f51-166">Например, если вы изменили размер кластера, добавив дополнительные узлы, повторная балансировка позволит топологии использовать новые узлы.</span><span class="sxs-lookup"><span data-stu-id="78f51-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="78f51-167">Для повторной балансировки топологии используйте кнопку __Rebalance__ (Перераспределить) в верхней части окна __Topology Summary__ (Сводка топологии).</span><span class="sxs-lookup"><span data-stu-id="78f51-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="78f51-168">При повторной балансировке сначала деактивируется топология, затем рабочие роли равномерно перераспределяются по кластеру и, наконец, топология возвращается в состояние, в котором она находилась перед повторной балансировкой.</span><span class="sxs-lookup"><span data-stu-id="78f51-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="78f51-169">Поэтому, если топология была активна, она снова становится активной.</span><span class="sxs-lookup"><span data-stu-id="78f51-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="78f51-170">Если она была отключена, то останется таковой.</span><span class="sxs-lookup"><span data-stu-id="78f51-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="78f51-171">Завершение работы топологии</span><span class="sxs-lookup"><span data-stu-id="78f51-171">Kill a topology</span></span>

<span data-ttu-id="78f51-172">Топологии Storm выполняются, пока не будут удалены или пока не будет удален кластер.</span><span class="sxs-lookup"><span data-stu-id="78f51-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="78f51-173">Чтобы остановить топологию, используйте кнопку __Прервать__ в верхней части окна __Topology Summary__ (Сводка топологии).</span><span class="sxs-lookup"><span data-stu-id="78f51-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="78f51-174">Мониторинг и управление: SSH и команда Storm</span><span class="sxs-lookup"><span data-stu-id="78f51-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="78f51-175">Программа `storm` позволяет работать с запущенными топологиями из командной строки.</span><span class="sxs-lookup"><span data-stu-id="78f51-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="78f51-176">Чтобы вывести полный список команд, воспользуйтесь `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="78f51-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="78f51-177">Вывод списка топологий</span><span class="sxs-lookup"><span data-stu-id="78f51-177">List topologies</span></span>

<span data-ttu-id="78f51-178">Чтобы просмотреть список всех запущенных топологий, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="78f51-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="78f51-179">Эта команда возвращает сведения аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="78f51-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="78f51-180">Деактивация и повторная активация</span><span class="sxs-lookup"><span data-stu-id="78f51-180">Deactivate and reactivate</span></span>

<span data-ttu-id="78f51-181">Деактивация топологии приостанавливает ее до завершения или повторной активации.</span><span class="sxs-lookup"><span data-stu-id="78f51-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="78f51-182">Чтобы отключить и повторно активировать топологию, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="78f51-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="78f51-183">Завершение запущенной топологии</span><span class="sxs-lookup"><span data-stu-id="78f51-183">Kill a running topology</span></span>

<span data-ttu-id="78f51-184">Топологии Storm после запуска продолжают работать до тех пор, пока не будут остановлены.</span><span class="sxs-lookup"><span data-stu-id="78f51-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="78f51-185">Для завершения топологии введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="78f51-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="78f51-186">Повторная балансировка</span><span class="sxs-lookup"><span data-stu-id="78f51-186">Rebalance</span></span>

<span data-ttu-id="78f51-187">Повторная балансировка топологии позволяет системе пересмотреть параллелизм топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="78f51-188">Например, если вы изменили размер кластера, добавив дополнительные узлы, повторная балансировка позволит топологии использовать новые узлы.</span><span class="sxs-lookup"><span data-stu-id="78f51-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="78f51-189">При повторной балансировке сначала деактивируется топология, затем рабочие роли равномерно перераспределяются по кластеру и, наконец, топология возвращается в состояние, в котором она находилась перед повторной балансировкой.</span><span class="sxs-lookup"><span data-stu-id="78f51-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="78f51-190">Поэтому, если топология была активна, она снова становится активной.</span><span class="sxs-lookup"><span data-stu-id="78f51-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="78f51-191">Если она была отключена, то останется таковой.</span><span class="sxs-lookup"><span data-stu-id="78f51-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="78f51-192">Мониторинг и управление: пользовательский интерфейс Storm</span><span class="sxs-lookup"><span data-stu-id="78f51-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="78f51-193">Пользовательский интерфейс Storm предоставляет веб-интерфейс для работы с запущенными топологиями и включен в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="78f51-194">Чтобы открыть пользовательский интерфейс Storm, в веб-браузере перейдите по адресу **https://CLUSTERNAME.azurehdinsight.net/stormui**, где **CLUSTERNAME** — это имя вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="78f51-195">При появлении соответствующего запроса введите имя пользователя и пароль администратора кластера (admin), которые использовались при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="78f51-196">Главная страница</span><span class="sxs-lookup"><span data-stu-id="78f51-196">Main page</span></span>

<span data-ttu-id="78f51-197">На главной странице пользовательского интерфейса Storm отображается следующая информация.</span><span class="sxs-lookup"><span data-stu-id="78f51-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="78f51-198">**Cluster summary**(Сводка по кластерам) — основная информация о кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="78f51-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="78f51-199">**Topology summary**(Сводка по топологиям) — список запущенных топологий.</span><span class="sxs-lookup"><span data-stu-id="78f51-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="78f51-200">С помощью ссылок в этом разделе можно просмотреть дополнительную информацию о конкретных топологиях.</span><span class="sxs-lookup"><span data-stu-id="78f51-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="78f51-201">**Supervisor summary**(Сводка по контролеру) — информация о контролере Storm.</span><span class="sxs-lookup"><span data-stu-id="78f51-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="78f51-202">**Nimbus configuration**(Конфигурация Nimbus) — конфигурация Nimbus для кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="78f51-203">Topology summary</span><span class="sxs-lookup"><span data-stu-id="78f51-203">Topology summary</span></span>

<span data-ttu-id="78f51-204">При выборе ссылки в разделе **Topology summary** (Сводка по топологиям) отображается следующая информация о топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="78f51-205">**Topology summary**(Сводка по топологии) — основная информация о топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="78f51-206">**Topology actions**(Действия с топологией) — действия управления, которые можно выполнять с топологией.</span><span class="sxs-lookup"><span data-stu-id="78f51-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="78f51-207">**Activate**(Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="78f51-208">**Deactivate**(Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="78f51-209">**Rebalance**(Повторная балансировка) — корректировка параллелизма топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="78f51-210">После изменения числа узлов в кластере необходимо выполнить повторную балансировку топологий.</span><span class="sxs-lookup"><span data-stu-id="78f51-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="78f51-211">Эта операция позволяет топологии скорректировать параллелизм для компенсации увеличения или уменьшения количества узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="78f51-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="78f51-212">Дополнительные сведения см. в статье <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a> (Общие сведения о параллелизме топологии Storm).</span><span class="sxs-lookup"><span data-stu-id="78f51-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="78f51-213">**Kill**(Удалить) — останавливает выполнение топологии Storm по истечении заданного времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="78f51-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="78f51-214">**Topology stats**(Статистика топологии) — статистика по топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="78f51-215">С помощью ссылок в столбце **Window** (Окно) можно установить интервал времени для оставшихся записей на странице.</span><span class="sxs-lookup"><span data-stu-id="78f51-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="78f51-216">**Spouts**(Воронки) — используемые в топологии источники данных, которые называются воронками.</span><span class="sxs-lookup"><span data-stu-id="78f51-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="78f51-217">С помощью ссылок в этом разделе можно получить дополнительную информацию о конкретных воронках.</span><span class="sxs-lookup"><span data-stu-id="78f51-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="78f51-218">**Bolts**(Сита — используемые в топологии обработчики данных, которые называются ситами.</span><span class="sxs-lookup"><span data-stu-id="78f51-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="78f51-219">С помощью ссылок в этом разделе можно получить дополнительную информацию о конкретных ситах.</span><span class="sxs-lookup"><span data-stu-id="78f51-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="78f51-220">**Topology configuration**(Конфигурация топологии) — конфигурация выбранной топологии.</span><span class="sxs-lookup"><span data-stu-id="78f51-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="78f51-221">Сводка по воронкам и ситам</span><span class="sxs-lookup"><span data-stu-id="78f51-221">Spout and Bolt summary</span></span>

<span data-ttu-id="78f51-222">При выборе воронки в разделе **Spouts** (Воронки) или **Bolts** (Сита) отображается следующая информация о выбранном элементе.</span><span class="sxs-lookup"><span data-stu-id="78f51-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="78f51-223">**Component summary**(Сводка по компоненту) — основная информация о воронке или сите.</span><span class="sxs-lookup"><span data-stu-id="78f51-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="78f51-224">**Spout/Bolt stats**(Статистика по воронке или ситу) — статистика по воронке или ситу.</span><span class="sxs-lookup"><span data-stu-id="78f51-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="78f51-225">С помощью ссылок в столбце **Window** (Окно) можно установить интервал времени для оставшихся записей на странице.</span><span class="sxs-lookup"><span data-stu-id="78f51-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="78f51-226">**Input stats** (Статистика по входным данным, только сита) — информация о входных потоках, проходящих через сито.</span><span class="sxs-lookup"><span data-stu-id="78f51-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="78f51-227">**Output stats**(Статистика по выходным данным) — информация о потоках, создаваемых этой воронкой или ситом.</span><span class="sxs-lookup"><span data-stu-id="78f51-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="78f51-228">**Executors**(Исполнители) — информация об экземплярах воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="78f51-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="78f51-229">Выберите запись **Port** (Порт) для конкретного исполнителя, чтобы просмотреть журнал диагностической информации, созданный для этого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="78f51-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="78f51-230">**Errors**(Ошибки) — информация об ошибках для данной воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="78f51-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="78f51-231">Мониторинг и управление: REST API</span><span class="sxs-lookup"><span data-stu-id="78f51-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="78f51-232">Пользовательский интерфейс Storm построен на базе REST API, поэтому функциональность отслеживания и управления можно реализовать аналогичным образом с помощью API.</span><span class="sxs-lookup"><span data-stu-id="78f51-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="78f51-233">С помощью REST API можно создать пользовательские средства для отслеживания топологий Storm и управления ими.</span><span class="sxs-lookup"><span data-stu-id="78f51-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="78f51-234">Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="78f51-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="78f51-235">Следующая информация касается использования REST API с Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78f51-236">API-интерфейс REST для Storm не является общедоступным через Интернет, и обращаться к нему необходимо с помощью туннеля SSH на головной узел кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="78f51-237">Дополнительные сведения о создании и использовании туннеля SSH см. в статье [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="78f51-238">Базовый универсальный код ресурса</span><span class="sxs-lookup"><span data-stu-id="78f51-238">Base URI</span></span>

<span data-ttu-id="78f51-239">Базовый универсальный код ресурса (URI) для REST API в кластерах HDInsight под управлением Linux доступен на головном узле: **https://HEADNODEFQDN:8744/api/v1/** .</span><span class="sxs-lookup"><span data-stu-id="78f51-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="78f51-240">Доменное имя головного узла формируется при создании кластера и не является статическим.</span><span class="sxs-lookup"><span data-stu-id="78f51-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="78f51-241">Полное доменное имя (FQDN) головного узла кластера можно получить несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="78f51-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="78f51-242">**Из сеанса SSH.** Из сеанса SSH в кластер примените команду `headnode -f`.</span><span class="sxs-lookup"><span data-stu-id="78f51-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="78f51-243">**Из веб-интерфейса Ambari.** В верхней части страницы выберите **Services** (Службы), а затем — **Storm**.</span><span class="sxs-lookup"><span data-stu-id="78f51-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="78f51-244">На вкладке **Summary** (Сводка) выберите **Storm UI Server** (Сервер пользовательского интерфейса Storm).</span><span class="sxs-lookup"><span data-stu-id="78f51-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="78f51-245">Полное доменное имя узла, на котором запущены пользовательский интерфейс Storm и REST API, указано в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="78f51-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="78f51-246">**Из интерфейса REST API Ambari.** Используйте команду `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"`, чтобы получить сведения об узле с выполняемыми пользовательскими интерфейсами Storm и REST API.</span><span class="sxs-lookup"><span data-stu-id="78f51-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="78f51-247">Замените **PASSWORD** паролем администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="78f51-248">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="78f51-249">Запись host_name в ответе будет содержать полное доменное имя узла.</span><span class="sxs-lookup"><span data-stu-id="78f51-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="78f51-250">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="78f51-250">Authentication</span></span>

<span data-ttu-id="78f51-251">Для запросов REST API необходимо использовать **обычную проверку подлинности**с помощью имени и пароля администратора кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f51-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="78f51-252">Так как при обычной проверке подлинности данные отправляются открытым текстом, следует **всегда** использовать HTTPS для защиты связи с кластером.</span><span class="sxs-lookup"><span data-stu-id="78f51-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="78f51-253">Возвращаемые значения</span><span class="sxs-lookup"><span data-stu-id="78f51-253">Return values</span></span>

<span data-ttu-id="78f51-254">Информацию, возвращаемую REST API, можно использовать только в пределах кластера или виртуальной машины в одной виртуальной сети Azure, выполняющей функцию кластера.</span><span class="sxs-lookup"><span data-stu-id="78f51-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="78f51-255">Например, полное доменное имя (FQDN), возвращаемое для серверов Zookeeper, недоступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="78f51-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78f51-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78f51-256">Next Steps</span></span>

<span data-ttu-id="78f51-257">Теперь, когда вы узнали, как развертывать и отслеживать топологии с помощью панели мониторинга Storm, можно переходить к [разработке топологий на основе Java с помощью Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="78f51-258">Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="78f51-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
