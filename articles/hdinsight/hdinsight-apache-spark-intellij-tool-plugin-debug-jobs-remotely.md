---
title: "набор средств для IntelliJ - отладки приложений удаленно на HDInsight Spark aaaAzure | Документы Microsoft"
description: "Узнайте, как использовать средства HDInsight в набор средств Azure для IntelliJ tooremotely отладки приложений, работающих в кластерах HDInsight Spark через виртуальную частную сеть."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="4d02a-103">Используйте набор средств Azure для приложений toodebug IntelliJ удаленно на HDInsight Spark через виртуальную частную сеть</span><span class="sxs-lookup"><span data-stu-id="4d02a-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="4d02a-104">Мы рекомендуем hello способ отладки spark applicaltion удаленно с помощью ssh.</span><span class="sxs-lookup"><span data-stu-id="4d02a-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="4d02a-105">Инструкции см. в статье [Удаленная отладка приложений Spark в кластере HDInsight через SSH с помощью набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="4d02a-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="4d02a-106">В этой статье приводятся пошаговые инструкции о предоставлении toouse hello средства HDInsight в набор средств Azure для IntelliJ toosubmit задания Spark на HDInsight Spark кластера и затем выполните отладку удаленно с компьютера.</span><span class="sxs-lookup"><span data-stu-id="4d02a-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="4d02a-107">toodo таким образом, необходимо выполнить следующие общие действия hello:</span><span class="sxs-lookup"><span data-stu-id="4d02a-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="4d02a-108">Создание виртуальной сети Azure типа "сеть — сеть" или "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="4d02a-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="4d02a-109">Hello в этом документе предполагается использовать сетевой сайт сайт.</span><span class="sxs-lookup"><span data-stu-id="4d02a-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="4d02a-110">Создайте кластер Spark в HDInsight Azure, который является частью hello-сайтами Azure виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d02a-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="4d02a-111">Проверьте сетевое подключение hello между головному узлу кластера hello и рабочим столом.</span><span class="sxs-lookup"><span data-stu-id="4d02a-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="4d02a-112">Создание приложения Scala в IntelliJ IDEA и его настройка для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="4d02a-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="4d02a-113">Запускать и отлаживать приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d02a-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d02a-114">Prerequisites</span></span>
* <span data-ttu-id="4d02a-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="4d02a-115">An Azure subscription.</span></span> <span data-ttu-id="4d02a-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4d02a-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4d02a-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4d02a-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4d02a-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4d02a-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="4d02a-119">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="4d02a-119">Oracle Java Development kit.</span></span> <span data-ttu-id="4d02a-120">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="4d02a-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="4d02a-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4d02a-121">IntelliJ IDEA.</span></span> <span data-ttu-id="4d02a-122">В этой статье используется версия 2017.1.</span><span class="sxs-lookup"><span data-stu-id="4d02a-122">This article uses version 2017.1.</span></span> <span data-ttu-id="4d02a-123">Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="4d02a-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="4d02a-124">Средства HDInsight в наборе средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4d02a-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="4d02a-125">Средства HDInsight для IntelliJ доступны как часть средств Azure для IntelliJ hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="4d02a-126">Инструкции как tooinstall hello набора средств Azure см. в разделе [hello установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="4d02a-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="4d02a-127">Войдите в подписку Azure из IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4d02a-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="4d02a-128">Следуйте инструкциям hello [здесь](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="4d02a-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="4d02a-129">При выполнении приложения Spark Scala для удаленной отладки на компьютере Windows, может возникнуть исключение, как описано в статье [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) это происходит из-за отсутствующих tooa WinUtils.exe в Windows.</span><span class="sxs-lookup"><span data-stu-id="4d02a-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="4d02a-130">toowork возникновения этой ошибки необходимо [скачать hello исполняемый здесь](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) расположение tooa **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="4d02a-131">Затем необходимо добавить переменную среды **HADOOP_HOME** и задайте значение hello hello переменной слишком**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="4d02a-132">Шаг 1. Создание виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="4d02a-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="4d02a-133">Следуйте инструкциям hello hello ниже ссылки toocreate виртуальной сети Azure, а затем проверьте подключением hello hello desktop и виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="4d02a-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="4d02a-134">Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4d02a-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="4d02a-135">Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d02a-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="4d02a-136">Настроить подключение точка сеть tooa виртуальной сети, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d02a-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="4d02a-137">Шаг 2. Создание кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4d02a-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="4d02a-138">Также следует создать кластер Apache Spark на Azure HDInsight, являющегося частью hello, созданную виртуальную сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="4d02a-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="4d02a-139">Используйте hello информация, доступная [под управлением Linux, создания кластеров в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4d02a-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="4d02a-140">Как часть дополнительной конфигурации выберите виртуальную сеть Azure, созданную в предыдущем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="4d02a-141">Шаг 3: Проверьте подключение hello между головному узлу кластера hello и рабочего стола</span><span class="sxs-lookup"><span data-stu-id="4d02a-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="4d02a-142">Получите IP-адрес hello головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="4d02a-143">Откройте Ambari пользовательского интерфейса для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="4d02a-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="4d02a-144">Из колонки hello кластера, нажмите кнопку **мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="4d02a-146">Hello Ambari пользовательского интерфейса, в правом верхнем углу hello, щелкните **узлов**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="4d02a-148">Отобразится список головных узлов, рабочих узлов и узлов zookeeper.</span><span class="sxs-lookup"><span data-stu-id="4d02a-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="4d02a-149">Hello headnodes имеют hello **hn*** префикс.</span><span class="sxs-lookup"><span data-stu-id="4d02a-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="4d02a-150">Щелкните первый головному узлу hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-150">Click hello first headnode.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="4d02a-152">Hello нижней части страницы hello, которое открывается из hello **Сводка** поле копирования hello IP-адрес головному узлу hello и имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="4d02a-154">Включить hello IP-адрес и имя узла hello hello головному узлу toohello **узлов** файл на компьютере hello, который нужно toorun и hello Spark заданий для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="4d02a-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="4d02a-155">Это позволит вам toocommunicate с hello головному узлу с помощью hello IP-адрес, а также имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="4d02a-156">Откройте блокнот с повышенным уровнем разрешений.</span><span class="sxs-lookup"><span data-stu-id="4d02a-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="4d02a-157">В меню "файл" hello, выберите **откройте** , а затем toohello расположение файла hosts hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="4d02a-158">На компьютере под управлением Windows это папка `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="4d02a-159">Добавьте следующие toohello hello **узлов** файла.</span><span class="sxs-lookup"><span data-stu-id="4d02a-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="4d02a-160">С hello компьютера, подключенного toohello виртуальной сети Azure, используемой кластером HDInsight hello проверьте связи обоих headnodes hello, с помощью hello IP-адрес, а также имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="4d02a-161">SSH в hello головному узлу кластера с помощью инструкций hello в [кластера HDInsight tooan соединение, с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4d02a-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="4d02a-162">С hello головному узлу кластера проверьте связь с IP-адрес hello hello настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="4d02a-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="4d02a-163">Следует проверить подключение tooboth hello IP-адресов, назначенных toohello компьютера, один для hello сетевого подключения и hello других для hello виртуальной сети Azure, hello компьютер подключен к.</span><span class="sxs-lookup"><span data-stu-id="4d02a-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="4d02a-164">Повторите шаги hello для hello других головному узлу.</span><span class="sxs-lookup"><span data-stu-id="4d02a-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="4d02a-165">Шаг 4: Создание приложения Spark Scala со средствами HDInsight hello в набор средств Azure для IntelliJ и настройте его для удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="4d02a-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="4d02a-166">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="4d02a-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="4d02a-167">В hello нового диалогового окна, сделайте hello следующие варианты, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="4d02a-169">Hello левой панели выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="4d02a-170">Hello правой области выберите **Spark в HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="4d02a-171">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-171">Click **Next**.</span></span>
2. <span data-ttu-id="4d02a-172">В следующем окне приветствия укажите следующие сведения о проекте hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="4d02a-173">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="4d02a-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="4d02a-174">Для параметра **Project SDK** (Пакет SDK проекта) выберите Java 1.8 для кластера Spark 2.x или Java 1.7 для кластера Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="4d02a-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="4d02a-175">Для параметра **Spark Version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK Spark и пакета SDK Scala.</span><span class="sxs-lookup"><span data-stu-id="4d02a-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="4d02a-176">Если версия кластера spark hello ниже 2.0, выберите любые блестящие 1.x.</span><span class="sxs-lookup"><span data-stu-id="4d02a-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="4d02a-177">В противном случае следует выбрать Spark 2.x.</span><span class="sxs-lookup"><span data-stu-id="4d02a-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="4d02a-178">В этом примере используется Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="4d02a-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="4d02a-179">![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="4d02a-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="4d02a-180">Hello Spark проекта автоматически создаст артефакта.</span><span class="sxs-lookup"><span data-stu-id="4d02a-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="4d02a-181">артефакт hello toosee, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4d02a-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="4d02a-182">Из hello **файл** меню, нажмите кнопку **структура проекта**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="4d02a-183">В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** toosee hello по умолчанию артефакт, который будет создан.</span><span class="sxs-lookup"><span data-stu-id="4d02a-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="4d02a-184">![Создание JAR-файла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="4d02a-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="4d02a-185">Можно также создать свои собственные артефакта bly, щелкнув hello  **+**  значок, выделяются в выше рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="4d02a-186">Добавьте проект библиотеки tooyour.</span><span class="sxs-lookup"><span data-stu-id="4d02a-186">Add libraries tooyour project.</span></span> <span data-ttu-id="4d02a-187">Щелкните правой кнопкой мыши имя проекта hello в дереве проекта hello tooadd библиотеки и нажмите кнопку **открыть параметры модуля**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="4d02a-188">В hello **структура проекта** диалогового окна hello левой панели щелкните **библиотеки**, щелкните символ hello (+) и нажмите кнопку **из Maven**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Добавление библиотеки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="4d02a-190">В hello **загрузка библиотеки из репозитория Maven** диалогового окна поле, поиск и добавить следующие библиотеки hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="4d02a-191">Копировать `yarn-site.xml` и `core-site.xml` из hello головному узлу кластера и добавить его в проект toohello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="4d02a-192">Используйте следующие команды toocopy hello файлы hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="4d02a-193">Можно использовать [Cygwin](https://cygwin.com/install.html) toorun hello следующие `scp` команды toocopy hello файлы из кластера headnodes hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="4d02a-194">Так как мы уже добавлена hello кластера головному узлу IP адрес и имена узлов fo hello файл hosts на рабочем столе hello, мы используем hello **scp** команд в следующие способом hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="4d02a-195">Добавление проекта tooyour этих файлов, скопировав их в списке hello **/src** папки в дереве проекта, например `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="4d02a-196">Обновление hello `core-site.xml` toomake hello следующие отличия.</span><span class="sxs-lookup"><span data-stu-id="4d02a-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="4d02a-197">`core-site.xml`включает шифрование hello учетной записи хранилища ключей toohello связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="4d02a-198">В hello `core-site.xml` добавления проекта toohello, замените hello зашифрованный ключ с ключом hello фактического хранения, связанный с учетной записью хранилища по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="4d02a-199">Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4d02a-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="4d02a-200">Удалите следующую записей из hello hello `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="4d02a-201">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-201">Save hello file.</span></span>
7. <span data-ttu-id="4d02a-202">Добавьте класс hello Main для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4d02a-202">Add hello Main class for your application.</span></span> <span data-ttu-id="4d02a-203">Из hello **обозревателя проектов**, щелкните правой кнопкой мыши **src**, слишком точки**New**и нажмите кнопку **Scala класса**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="4d02a-205">В hello **создать новый класс Scala** диалогового окна введите имя, **вид** выберите **объекта**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="4d02a-207">В hello `MyClusterAppMain.scala` файл, вставьте следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="4d02a-208">Этот код создает контекст Spark hello и запускает `executeJob` метод hello `SparkSample` объекта.</span><span class="sxs-lookup"><span data-stu-id="4d02a-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="4d02a-209">Повторите шаги 8 и 9 над именем объекта Scala tooadd `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="4d02a-210">Класс toothis добавить hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="4d02a-210">toothis class add hello following code.</span></span> <span data-ttu-id="4d02a-211">Этот код считывает данные hello из hello HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру hello седьмой столбца в hello CSV и записывает выходные данные hello слишком**/HVACOut** в группе по умолчанию hello Контейнер хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="4d02a-212">Повторите шаги 8 и 9 выше tooadd новый класс с именем `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="4d02a-213">Этот класс реализует платформа тестирования hello Spark, которая используется для отладки приложений.</span><span class="sxs-lookup"><span data-stu-id="4d02a-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="4d02a-214">Добавьте следующий код toohello hello `RemoteClusterDebugging` класса.</span><span class="sxs-lookup"><span data-stu-id="4d02a-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="4d02a-215">Несколько важных событий toonote здесь:</span><span class="sxs-lookup"><span data-stu-id="4d02a-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="4d02a-216">Для `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, убедитесь, что hello Spark сборки JAR-ФАЙЛ можно найти в хранилище кластера hello по указанному пути hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="4d02a-217">Для `setJars`, укажите расположение hello, где будут создаваться jar артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="4d02a-218">Обычно это `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="4d02a-219">В hello `RemoteClusterDebugging` класса, щелкните правой кнопкой мыши hello `test` ключевое слово и выберите **Создание конфигурации RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="4d02a-221">В диалоговом окне приветствия укажите имя для конфигурации hello и выберите hello **проверить тип** как **имя теста**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="4d02a-222">Оставьте остальные значения, установленные по умолчанию, нажмите кнопку **Применить**, а затем — кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="4d02a-224">Теперь вы увидите **удаленного запуска** конфигурации раскрывающееся меню в строке меню hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="4d02a-226">Шаг 5: Запуск приложения hello в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="4d02a-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="4d02a-227">Откройте в проекте IntelliJ ИДЕЯ `SparkSample.scala` и создать точку останова следующей too'val rdd1 ".</span><span class="sxs-lookup"><span data-stu-id="4d02a-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="4d02a-228">Во всплывающем меню hello для создания точки останова, выберите **строку в функции executeJob**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Добавление точки останова](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="4d02a-230">Щелкните hello **отладки запуска** кнопку Далее toohello **удаленного запуска** toostart раскрывающийся список конфигурации запущено приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="4d02a-232">Когда выполнение программы hello достигает точки останова hello, вы увидите **отладчик** вкладку в нижней области hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="4d02a-234">Нажмите кнопку hello (**+**) tooadd значок контрольного значения, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="4d02a-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="4d02a-236">Здесь, так как приложение hello было передано до hello переменной `rdd1` был создан с помощью этого контрольного значения, мы видим, что являются hello первые 5 строк в переменную hello `rdd`.</span><span class="sxs-lookup"><span data-stu-id="4d02a-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="4d02a-237">Нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4d02a-237">Press **ENTER**.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="4d02a-239">В приведенном выше изображении hello это представление, во время выполнения, может запросить terrabytes данных и отладки как работы вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4d02a-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="4d02a-240">Например, в hello выводу, приведенному выше рисунке hello, вы увидите, hello первую строку hello выходных данных является заголовком.</span><span class="sxs-lookup"><span data-stu-id="4d02a-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="4d02a-241">Исходя из этого, можно изменить в строку заголовка кода tooskip приложения hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4d02a-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="4d02a-242">Теперь можно нажать hello **программы Resume** tooproceed значок с запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="4d02a-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="4d02a-244">Если приложение hello завершается успешно, вы увидите выход hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4d02a-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="4d02a-246"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4d02a-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4d02a-247">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d02a-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="4d02a-248">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="4d02a-248">Demo</span></span>
* <span data-ttu-id="4d02a-249">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="4d02a-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="4d02a-250">Удаленной отладки (видео): [используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно на кластер HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="4d02a-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="4d02a-251">Сценарии</span><span class="sxs-lookup"><span data-stu-id="4d02a-251">Scenarios</span></span>
* [<span data-ttu-id="4d02a-252">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="4d02a-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4d02a-253">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="4d02a-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4d02a-254">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="4d02a-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4d02a-255">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="4d02a-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4d02a-256">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d02a-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4d02a-257">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="4d02a-257">Create and run applications</span></span>
* [<span data-ttu-id="4d02a-258">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="4d02a-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4d02a-259">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="4d02a-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4d02a-260">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="4d02a-260">Tools and extensions</span></span>
* [<span data-ttu-id="4d02a-261">Использование средства HDInsight в набор средств Azure для IntelliJ toocreate и отправка Spark Scala основных приложений</span><span class="sxs-lookup"><span data-stu-id="4d02a-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4d02a-262">Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через SSH</span><span class="sxs-lookup"><span data-stu-id="4d02a-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="4d02a-263">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="4d02a-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="4d02a-264">Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений</span><span class="sxs-lookup"><span data-stu-id="4d02a-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="4d02a-265">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d02a-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4d02a-266">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d02a-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4d02a-267">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="4d02a-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4d02a-268">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4d02a-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4d02a-269">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="4d02a-269">Manage resources</span></span>
* [<span data-ttu-id="4d02a-270">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d02a-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4d02a-271">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="4d02a-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
