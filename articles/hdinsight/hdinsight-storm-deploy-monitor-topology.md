---
title: "aaaDeploy и управления ими Apache Storm топологии на HDInsight | Документы Microsoft"
description: "Узнайте, как toodeploy, мониторинг и управление ими с помощью панели мониторинга Storm hello в HDInsight топологии Apache Storm. Использование инструментов Hadoop для Visual Studio."
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
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="5bcc2-104">Развертывание топологий Apache Storm в HDInsight под управлением Windows и управление ими</span><span class="sxs-lookup"><span data-stu-id="5bcc2-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="5bcc2-105">Hello Storm панель мониторинга позволяет tooeasily развернуть и запустить кластер HDInsight tooyour Apache Storm топологии с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="5bcc2-106">Можно также использовать панель мониторинга toomonitor hello и управлять выполняющегося топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="5bcc2-107">Если вы используете Visual Studio, hello средства HDInsight для Visual Studio предоставляет аналогичные функциональные возможности в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="5bcc2-108">Hello Storm панели мониторинга и функции hello ураган в hello средства HDInsight используют hello Storm REST API, который можно использовать toocreate своих собственных решениях, мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bcc2-109">Hello в данном пошаговом руководстве требуется ураган в кластере HDInsight, который использует Windows hello операционной системой.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="5bcc2-110">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5bcc2-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="5bcc2-112">Сведения о развертывании топологий Storm и управлении ими с помощью кластера HDInsight под управлением Linux см. в статье [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bcc2-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5bcc2-113">Prerequisites</span></span>

* <span data-ttu-id="5bcc2-114">**Apache Storm в HDInsight** — инструкции по созданию кластера представлены в статье [Начало работы с Apache Storm в HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="5bcc2-115">Для hello **Storm мониторинга**: современных веб-браузер, поддерживающий HTML5.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="5bcc2-116">Для **Visual Studio** -пакета Azure SDK 2.5.1 или более поздней версии и hello средства HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="5bcc2-117">В разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall и настройте hello средства HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="5bcc2-118">Одно из следующих версий Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="5bcc2-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="5bcc2-119">Visual Studio 2012 с обновлением 4;</span><span class="sxs-lookup"><span data-stu-id="5bcc2-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="5bcc2-120">Visual Studio 2013 с обновлением 4 или Visual Studio 2013 Community;</span><span class="sxs-lookup"><span data-stu-id="5bcc2-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="5bcc2-121">Visual Studio 2015 (любой выпуск);</span><span class="sxs-lookup"><span data-stu-id="5bcc2-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="5bcc2-122">Visual Studio 2017 (любой выпуск).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="5bcc2-123">Панель мониторинга Storm</span><span class="sxs-lookup"><span data-stu-id="5bcc2-123">Storm Dashboard</span></span>

<span data-ttu-id="5bcc2-124">Hello Storm панели мониторинга — веб-страница, доступных в вашем кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="5bcc2-125">URL-адрес Hello **https://&lt;имя_кластера >.azurehdinsight.net/**, где **clustername** — имя вашего ураган в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="5bcc2-126">С помощью hello hello Storm панели мониторинга, выберите **отправить топологии**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="5bcc2-127">Следуйте hello инструкции на странице приветствия toorun пример топологии или tooupload и запустите топологии, созданный вами.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Топология страница отправки Hello][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="5bcc2-129">Пользовательский интерфейс Storm</span><span class="sxs-lookup"><span data-stu-id="5bcc2-129">Storm UI</span></span>

<span data-ttu-id="5bcc2-130">Hello Storm панели мониторинга, выберите hello **Storm пользовательского интерфейса** ссылку.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="5bcc2-131">Отобразятся сведения о кластере hello в tooany сложения под управлением топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![пользовательский интерфейс storm Hello][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="5bcc2-133">В некоторых версиях Internet Explorer может оказаться, что hello Storm пользовательского интерфейса не обновляется после его сначала посещения.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="5bcc2-134">Например не может отображаться новый топологии hello отправленные вами или топологии активным может отображаться при его предшествующей деактивации.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="5bcc2-135">Корпорация Майкрософт знает о наличии этой проблемы и работает над ее решением.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="5bcc2-136">Главная страница</span><span class="sxs-lookup"><span data-stu-id="5bcc2-136">Main page</span></span>

<span data-ttu-id="5bcc2-137">Главная страница Hello hello Storm пользовательского интерфейса предоставляет hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="5bcc2-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="5bcc2-138">**Сводка кластера**: основные сведения о кластере Storm hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="5bcc2-139">**Topology summary**(Сводка по топологиям) — список запущенных топологий.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="5bcc2-140">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="5bcc2-141">**Допуск сводки**: сведения о начальника Storm hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="5bcc2-142">**Конфигурация nimbus**: Nimbus конфигурации для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="5bcc2-143">Topology summary</span><span class="sxs-lookup"><span data-stu-id="5bcc2-143">Topology summary</span></span>

<span data-ttu-id="5bcc2-144">При выборе ссылки из hello **топологии Сводка** разделе отображаются следующие сведения о топологии hello hello:</span><span class="sxs-lookup"><span data-stu-id="5bcc2-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="5bcc2-145">**Сводка топологии**: основные сведения о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="5bcc2-146">**Топология действия**: операции управления, которые можно выполнять для топологии hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="5bcc2-147">**Activate**(Включить) — возобновление обработки отключенной топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="5bcc2-148">**Deactivate**(Отключить) — приостановка выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="5bcc2-149">**Перебалансировка**: корректирует параллелизм hello hello топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="5bcc2-150">После изменения hello количество узлов в кластере hello следует производят повторную балансировку выполняющегося топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="5bcc2-151">Это позволяет toocompensate hello топологии tooadjust параллелизма для hello увеличивается или уменьшается число узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="5bcc2-152">Дополнительные сведения см. в разделе [основные сведения о параллелизма hello топологии Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="5bcc2-153">**KILL**: завершает топологии Storm после hello указано время ожидания.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="5bcc2-154">**Топология stats**: статистические данные о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="5bcc2-155">Используйте ссылки hello в hello **окна** столбца tooset hello временные рамки hello оставшихся записей на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="5bcc2-156">**Spouts**: hello spouts используемой топологии hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="5bcc2-157">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных spouts.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="5bcc2-158">**Болтов**: hello винты используемой топологии hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="5bcc2-159">Используйте ссылки hello в этот раздел tooview Дополнительные сведения о конкретных винты.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="5bcc2-160">**Конфигурация топологии**: hello конфигурации hello выбранной топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="5bcc2-161">Сводка по воронкам и ситам</span><span class="sxs-lookup"><span data-stu-id="5bcc2-161">Spout and Bolt summary</span></span>

<span data-ttu-id="5bcc2-162">Выбрав spout hello **Spouts** или **болтов** разделы отображает hello следующую информацию о hello выбранного элемента:</span><span class="sxs-lookup"><span data-stu-id="5bcc2-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="5bcc2-163">**Сводка компонентов**: основные сведения о hello spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="5bcc2-164">**Spout/молнии stats**: статистику hello spout или винта.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="5bcc2-165">Используйте ссылки hello в hello **окна** столбца tooset hello временные рамки hello оставшихся записей на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="5bcc2-166">**Статистика ввода** (только винта): сведения о hello входные потоки, используемые hello молнии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="5bcc2-167">**Выходные данные статистики**: сведения о потоках hello, генерируемой это spout или винта.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="5bcc2-168">**Исполнители**: сведения об экземплярах hello hello spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="5bcc2-169">Выберите hello **порт** запись для tooview определенного исполнителя, создается журнал диагностических сведений для данного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="5bcc2-170">**Errors**(Ошибки) — информация об ошибках для данной воронки или сита.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="5bcc2-171">Средства HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bcc2-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="5bcc2-172">Средства HDInsight Hello может быть используется toosubmit C# или гибридной топологии tooyour Storm кластера.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="5bcc2-173">следующие шаги Hello используйте образец приложения.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-173">hello following steps use a sample application.</span></span> <span data-ttu-id="5bcc2-174">Сведения о создании собственных топологий с помощью средства HDInsight hello см. в разделе [топологии разработки C# с помощью hello средства HDInsight для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="5bcc2-175">Используйте следующие шаги toodeploy пример tooyour Storm в кластере HDInsight hello просматривать и управлять топологией hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="5bcc2-176">Если вы уже установили hello последнюю версию hello средства HDInsight для Visual Studio, в разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="5bcc2-177">Откройте Visual Studio b выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="5bcc2-178">В hello **новый проект** диалогового окна разверните **установленные** > **шаблоны**, а затем выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="5bcc2-179">Выберите из списка шаблонов hello **Storm пример**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="5bcc2-180">Внизу hello диалогового окна «hello» введите имя для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![изображение](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="5bcc2-182">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bcc2-183">Если необходимо, введите учетные данные входа hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="5bcc2-184">При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="5bcc2-185">Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="5bcc2-186">Можно отслеживать факт отправки hello выполнена с помощью hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="5bcc2-187">При успешной отправки топологии hello hello **Storm топологии** для hello кластера должны отображаться.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="5bcc2-188">Выберите топологию hello hello список tooview сведения о hello под управлением топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![мониторинг Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="5bcc2-190">Можно также просмотреть **топологии Storm** в **обозревателе серверов**. Для этого разверните **Azure** > **HDInsight**, затем щелкните правой кнопкой мыши топологию Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="5bcc2-191">Выберите фигуру hello для hello spouts или болтов tooview сведения об этих компонентах.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="5bcc2-192">Для каждого выбранного элемента открывается новое окно.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bcc2-193">Имя Hello hello топологии — имя класса hello hello топологии (в этом случае `HelloWord`,) с меткой времени добавляется.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="5bcc2-194">Из hello **топологии Сводка** представление, выберите **Kill** toostop hello топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bcc2-195">Топологии storm продолжения, пока они не будут остановлены или hello кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="5bcc2-196">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="5bcc2-196">REST API</span></span>

<span data-ttu-id="5bcc2-197">Hello пользовательского интерфейса Storm построено на основе hello REST API, чтобы выполнить аналогичные отслеживание и управление ими функциональные возможности с помощью API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="5bcc2-198">Hello API-интерфейса REST toocreate пользовательские средства можно использовать для управления и мониторинга Storm топологии.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="5bcc2-199">Дополнительные сведения см. в разделе [API-интерфейс REST пользовательского интерфейса Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="5bcc2-200">Hello следующие сведения являются hello конкретных toousing API REST с Apache Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="5bcc2-201">Базовый универсальный код ресурса</span><span class="sxs-lookup"><span data-stu-id="5bcc2-201">Base URI</span></span>

<span data-ttu-id="5bcc2-202">базовый URI для hello REST API в кластерах HDInsight Hello **https://&lt;имя_кластера >.azurehdinsight.net/stormui/api/v1/**, где **clustername** — имя вашего Storm hello на Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="5bcc2-203">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="5bcc2-203">Authentication</span></span>

<span data-ttu-id="5bcc2-204">Toohello запросы, необходимо использовать API-Интерфейс REST **обычной проверки подлинности**, поэтому использовать hello HDInsight кластер имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="5bcc2-205">Поскольку обычная проверка подлинности передается с помощью открытого текста, следует **всегда** использовать кластере hello toosecure подключений по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="5bcc2-206">Возвращаемые значения</span><span class="sxs-lookup"><span data-stu-id="5bcc2-206">Return values</span></span>

<span data-ttu-id="5bcc2-207">Сведения, возвращаемые из hello API-интерфейса REST только может быть одновременно доступен из кода внутри кластера hello или виртуальных машин на hello одной виртуальной сети Azure как кластер hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="5bcc2-208">Например hello полное доменное имя (FQDN), возвращаемое для Zookeeper серверы являются недоступна из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="5bcc2-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bcc2-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5bcc2-209">Next Steps</span></span>

<span data-ttu-id="5bcc2-210">Теперь, когда вы узнали, как монитор и toodeploy топологии с помощью hello Storm панели мониторинга, узнайте, как:</span><span class="sxs-lookup"><span data-stu-id="5bcc2-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="5bcc2-211">Разработка топологии C# с помощью hello средства HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bcc2-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="5bcc2-212">Разработка топологий на платформе Java с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="5bcc2-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="5bcc2-213">Другие примеры топологий Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5bcc2-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
