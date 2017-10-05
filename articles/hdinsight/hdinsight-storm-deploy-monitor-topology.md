---
title: "Развертывание топологий Apache Storm в HDInsight и управление ими | Документация Майкрософт"
description: "Узнайте, как развертывать и отслеживать топологии Apache Storm, а также управлять ими с помощью панели мониторинга Storm в HDInsight. Использование инструментов Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="7b704-104">Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими</span><span class="sxs-lookup"><span data-stu-id="7b704-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="7b704-105">Панель мониторинга Storm позволяет легко развернуть и запустить топологии Apache Storm в кластере HDInsight с помощью браузера.</span><span class="sxs-lookup"><span data-stu-id="7b704-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="7b704-106">С помощью панели мониторинга можно также следить за топологиями и управлять их работой.</span><span class="sxs-lookup"><span data-stu-id="7b704-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="7b704-107">Если используется Visual Studio, средства HDInsight для Visual Studio предоставляют аналогичные функциональные возможности в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b704-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="7b704-108">Панель мониторинга и компоненты Storm в средствах HDInsight используют интерфейс REST API для Storm, с помощью которого можно создавать собственные решения для мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="7b704-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b704-109">Действия, описанные в этом документе, требуют наличия Storm в кластере HDInsight с операционной системой Windows.</span><span class="sxs-lookup"><span data-stu-id="7b704-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="7b704-110">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7b704-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7b704-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7b704-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="7b704-112">Сведения о развертывании топологий Storm и управлении ими с помощью кластера HDInsight под управлением Linux см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b704-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7b704-113">Prerequisites</span></span>

* <span data-ttu-id="7b704-114">**Apache Storm в HDInsight** — инструкции по созданию кластера представлены в статье [Начало работы с Apache Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="7b704-115">Для **панели мониторинга Storm**— современный браузер, который поддерживает HTML5.</span><span class="sxs-lookup"><span data-stu-id="7b704-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="7b704-116">Для **Visual Studio** — пакет SDK для Azure 2.5.1 или более поздней версии и средства HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b704-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="7b704-117">Инструкции по установке и настройке средств HDInsight для Visual Studio см. в статье [Начало работы со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="7b704-118">Одна из следующих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7b704-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="7b704-119">Visual Studio 2012 с обновлением 4;</span><span class="sxs-lookup"><span data-stu-id="7b704-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="7b704-120">Visual Studio 2013 с обновлением 4 или Visual Studio 2013 Community;</span><span class="sxs-lookup"><span data-stu-id="7b704-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="7b704-121">Visual Studio 2015 (любой выпуск);</span><span class="sxs-lookup"><span data-stu-id="7b704-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="7b704-122">Visual Studio 2017 (любой выпуск).</span><span class="sxs-lookup"><span data-stu-id="7b704-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="7b704-123">Панель мониторинга Storm</span><span class="sxs-lookup"><span data-stu-id="7b704-123">Storm Dashboard</span></span>

<span data-ttu-id="7b704-124">Панель мониторинга Storm представляет собой веб-страницу в кластере Storm</span><span class="sxs-lookup"><span data-stu-id="7b704-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="7b704-125">URL-адрес: **https://&lt;имя_кластера>.azurehdinsight.net/**, где **имя_кластера** — это имя топологии Storm в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b704-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="7b704-126">В верхней части панели мониторинга Storm выберите **Submit Topology**(Отправка топологии).</span><span class="sxs-lookup"><span data-stu-id="7b704-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="7b704-127">Следуйте инструкциям на странице, чтобы запустить пример топологии или передать и запустить созданную вами топологию.</span><span class="sxs-lookup"><span data-stu-id="7b704-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![страница отправки топологии][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="7b704-129">Пользовательский интерфейс Storm</span><span class="sxs-lookup"><span data-stu-id="7b704-129">Storm UI</span></span>

<span data-ttu-id="7b704-130">На панели мониторинга Storm выберите ссылку **Storm UI** (Пользовательский интерфейс Storm).</span><span class="sxs-lookup"><span data-stu-id="7b704-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="7b704-131">Отобразятся сведения о кластере, а также о всех запущенных топологиях.</span><span class="sxs-lookup"><span data-stu-id="7b704-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![пользовательский интерфейс storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="7b704-133">В некоторых версиях Internet Explorer может возникать ситуация, когда пользовательский интерфейс Storm не обновляется после первого открытия.</span><span class="sxs-lookup"><span data-stu-id="7b704-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="7b704-134">Например, он может не отображать новые отправленные топологии или отображать топологию как активную, хотя она была выключена.</span><span class="sxs-lookup"><span data-stu-id="7b704-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="7b704-135">Корпорация Майкрософт знает о наличии этой проблемы и работает над ее решением.</span><span class="sxs-lookup"><span data-stu-id="7b704-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="7b704-136">Главная страница</span><span class="sxs-lookup"><span data-stu-id="7b704-136">Main page</span></span>

<span data-ttu-id="7b704-137">На главной странице пользовательского интерфейса Storm отображается следующая информация.</span><span class="sxs-lookup"><span data-stu-id="7b704-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="7b704-138">**Cluster summary**(Сводка по кластерам) — основная информация о кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="7b704-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="7b704-139">**Topology summary**(Сводка по топологиям) — список запущенных топологий.</span><span class="sxs-lookup"><span data-stu-id="7b704-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="7b704-140">С помощью ссылок в этом разделе можно просмотреть дополнительную информацию о конкретных топологиях.</span><span class="sxs-lookup"><span data-stu-id="7b704-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="7b704-141">**Supervisor summary**(Сводка по контролеру) — информация о контролере Storm.</span><span class="sxs-lookup"><span data-stu-id="7b704-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="7b704-142">**Nimbus configuration**(Конфигурация Nimbus) — конфигурация Nimbus для кластера.</span><span class="sxs-lookup"><span data-stu-id="7b704-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="7b704-143">Topology summary</span><span class="sxs-lookup"><span data-stu-id="7b704-143">Topology summary</span></span>

<span data-ttu-id="7b704-144">При выборе ссылки в разделе **Topology summary** (Сводка по топологиям) отображается следующая информация о топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="7b704-145">**Topology summary**(Сводка по топологии) — основная информация о топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="7b704-146">**Topology actions**(Действия с топологией) — действия управления, которые можно выполнять с топологией.</span><span class="sxs-lookup"><span data-stu-id="7b704-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="7b704-147">**Activate**(Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="7b704-148">**Deactivate**(Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="7b704-149">**Rebalance**(Повторная балансировка) — корректировка параллелизма топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="7b704-150">После изменения числа узлов в кластере необходимо выполнить повторную балансировку топологий.</span><span class="sxs-lookup"><span data-stu-id="7b704-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="7b704-151">Это позволяет топологии скорректировать параллелизм для компенсации увеличения или уменьшения количества узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="7b704-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="7b704-152">Дополнительные сведения см. в разделе [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (Основные сведения о параллелизме в топологии Storm): http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html.</span><span class="sxs-lookup"><span data-stu-id="7b704-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="7b704-153">**Kill**(Удалить) — останавливает выполнение топологии Storm по истечении заданного времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="7b704-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="7b704-154">**Topology stats**(Статистика топологии) — статистика по топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="7b704-155">С помощью ссылок в столбце **Window** (Окно) можно установить временные рамки для оставшихся записей на странице.</span><span class="sxs-lookup"><span data-stu-id="7b704-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="7b704-156">**Spouts**(Воронки) — используемые в топологии источники данных, которые называются воронками.</span><span class="sxs-lookup"><span data-stu-id="7b704-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="7b704-157">С помощью ссылок в этом разделе можно получить дополнительную информацию о конкретных воронках.</span><span class="sxs-lookup"><span data-stu-id="7b704-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="7b704-158">**Bolts**(Сита — используемые в топологии обработчики данных, которые называются ситами.</span><span class="sxs-lookup"><span data-stu-id="7b704-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="7b704-159">С помощью ссылок в этом разделе можно получить дополнительную информацию о конкретных ситах.</span><span class="sxs-lookup"><span data-stu-id="7b704-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="7b704-160">**Topology configuration**(Конфигурация топологии) — конфигурация выбранной топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="7b704-161">Сводка по воронкам и ситам</span><span class="sxs-lookup"><span data-stu-id="7b704-161">Spout and Bolt summary</span></span>

<span data-ttu-id="7b704-162">При выборе воронки в разделе **Spouts** (Воронки) или **Bolts** (Сита) отображается следующая информация о выбранном элементе.</span><span class="sxs-lookup"><span data-stu-id="7b704-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="7b704-163">**Component summary**(Сводка по компоненту) — основная информация о воронке или сите.</span><span class="sxs-lookup"><span data-stu-id="7b704-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="7b704-164">**Spout/Bolt stats**(Статистика по воронке или ситу) — статистика по воронке или ситу.</span><span class="sxs-lookup"><span data-stu-id="7b704-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="7b704-165">С помощью ссылок в столбце **Window** (Окно) можно установить временные рамки для оставшихся записей на странице.</span><span class="sxs-lookup"><span data-stu-id="7b704-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="7b704-166">**Input stats** (Статистика по входным данным, только сита) — информация о входных потоках, проходящих через сито.</span><span class="sxs-lookup"><span data-stu-id="7b704-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="7b704-167">**Output stats**(Статистика по выходным данным) — информация о потоках, создаваемых этой воронкой или ситом.</span><span class="sxs-lookup"><span data-stu-id="7b704-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="7b704-168">**Executors**(Исполнители) — информация об экземплярах воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="7b704-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="7b704-169">Выберите запись **Port** (Порт) для конкретного исполнителя, чтобы просмотреть журнал диагностической информации, созданный для этого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="7b704-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="7b704-170">**Errors**(Ошибки) — информация об ошибках для данной воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="7b704-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="7b704-171">Средства HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b704-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="7b704-172">Средства HDInsight можно использовать для отправки топологии C# или гибридной топологии в кластер Storm.</span><span class="sxs-lookup"><span data-stu-id="7b704-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="7b704-173">Далее используется пример приложения.</span><span class="sxs-lookup"><span data-stu-id="7b704-173">The following steps use a sample application.</span></span> <span data-ttu-id="7b704-174">Информацию о создании собственных топологий с помощью средств HDInsight см. в разделе [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="7b704-175">Чтобы развернуть пример в Storm в кластере HDInsight, а затем просмотреть топологию и управлять ею, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="7b704-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="7b704-176">Если вы еще не установили последнюю версию средств HDInsight для Visual Studio, см. статью [Начало работы со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="7b704-177">Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="7b704-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="7b704-178">В диалоговом окне **Новый проект** разверните **Установленные** > **Шаблоны** и выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7b704-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="7b704-179">В списке шаблонов выберите **Пример Storm**.</span><span class="sxs-lookup"><span data-stu-id="7b704-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="7b704-180">В нижней части диалогового окна введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="7b704-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="7b704-182">В **обозревателе решений** щелкните правой кнопкой мыши проект и выберите **Submit to Storm on HDInsight** (Отправить в Storm в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="7b704-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b704-183">При появлении запроса введите учетные данные входа для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7b704-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="7b704-184">Если у вас несколько подписок, воспользуйтесь той, что содержит ваш кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b704-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="7b704-185">Выберите Storm в кластере HDInsight из раскрывающегося списка **Кластер Storm** и щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="7b704-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="7b704-186">Вы можете отслеживать выполнение отправки в окне **Выходные данные** .</span><span class="sxs-lookup"><span data-stu-id="7b704-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="7b704-187">После успешной отправки топологии должны появиться **топологии Storm** для кластера.</span><span class="sxs-lookup"><span data-stu-id="7b704-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="7b704-188">Выберите топологию в списке, чтобы просмотреть информацию о выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="7b704-188">Select the topology from the list to view information about the running topology.</span></span>

    ![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="7b704-190">Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="7b704-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="7b704-191">Выделите компонент spout или bolt, чтобы просмотреть информацию о нем.</span><span class="sxs-lookup"><span data-stu-id="7b704-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="7b704-192">Для каждого выбранного элемента открывается новое окно.</span><span class="sxs-lookup"><span data-stu-id="7b704-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b704-193">Имя топологии — это имя класса топологии (в данном случае `HelloWord`) с добавлением отметки времени.</span><span class="sxs-lookup"><span data-stu-id="7b704-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="7b704-194">В представлении **Topology Summary** (Сводка по топологиям) выберите **Прервать**, чтобы остановить топологию.</span><span class="sxs-lookup"><span data-stu-id="7b704-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b704-195">Топологии Storm выполняются, пока не будут удалены или пока не будет удален кластер.</span><span class="sxs-lookup"><span data-stu-id="7b704-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="7b704-196">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="7b704-196">REST API</span></span>

<span data-ttu-id="7b704-197">Пользовательский интерфейс Storm построен на базе REST API, поэтому функциональность отслеживания и управления можно реализовать аналогичным образом с помощью API.</span><span class="sxs-lookup"><span data-stu-id="7b704-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="7b704-198">С помощью REST API можно создать пользовательские средства для отслеживания топологий Storm и управления ими.</span><span class="sxs-lookup"><span data-stu-id="7b704-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="7b704-199">Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="7b704-200">Следующая информация касается использования REST API с Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b704-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="7b704-201">Базовый универсальный код ресурса</span><span class="sxs-lookup"><span data-stu-id="7b704-201">Base URI</span></span>

<span data-ttu-id="7b704-202">Базовый универсальный код ресурса (URI) для REST API в кластерах HDInsight: **https://&lt;имя_кластера>.azurehdinsight.net/stormui/api/v1/**, где **имя_кластера** — это имя топологии Storm в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b704-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="7b704-203">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="7b704-203">Authentication</span></span>

<span data-ttu-id="7b704-204">Для запросов REST API необходимо использовать **обычную проверку подлинности**с помощью имени и пароля администратора кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b704-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="7b704-205">Так как при обычной проверке подлинности данные отправляются открытым текстом, следует **всегда** использовать HTTPS для защиты связи с кластером.</span><span class="sxs-lookup"><span data-stu-id="7b704-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="7b704-206">Возвращаемые значения</span><span class="sxs-lookup"><span data-stu-id="7b704-206">Return values</span></span>

<span data-ttu-id="7b704-207">Информацию, возвращаемую REST API, можно использовать только в пределах кластера или виртуальной машины в одной виртуальной сети Azure, выполняющей функцию кластера.</span><span class="sxs-lookup"><span data-stu-id="7b704-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="7b704-208">Например, полное доменное имя (FQDN), возвращаемое для серверов Zookeeper, недоступно из Интернета.</span><span class="sxs-lookup"><span data-stu-id="7b704-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b704-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b704-209">Next Steps</span></span>

<span data-ttu-id="7b704-210">Теперь, когда вы знаете принципы развертывания и мониторинга топологии с помощью панели мониторинга Storm, вы можете ознакомиться с другими сведениями.</span><span class="sxs-lookup"><span data-stu-id="7b704-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="7b704-211">Развертывание топологий C# с помощью средств HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b704-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="7b704-212">Разработка топологий на платформе Java с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="7b704-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="7b704-213">Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7b704-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
