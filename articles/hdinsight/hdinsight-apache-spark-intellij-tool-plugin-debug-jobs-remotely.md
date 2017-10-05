---
title: "Удаленная отладка приложений в HDInsight Spark с помощью набора средств Azure для IntelliJ | Документация Майкрософт"
description: "Узнайте, как использовать средства HDInsight в наборе средств Azure для IntelliJ для удаленной отладки приложений Spark в кластерах HDInsight Spark через VPN."
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="127a8-103">Удаленная отладка приложений в HDInsight Spark через VPN с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="127a8-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="127a8-104">Для удаленной отладки приложений Spark мы рекомендуем использовать SSH.</span><span class="sxs-lookup"><span data-stu-id="127a8-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="127a8-105">Инструкции см. в статье [Удаленная отладка приложений Spark в кластере HDInsight через SSH с помощью набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="127a8-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="127a8-106">В этой статье приводятся пошаговые инструкции по использованию средств HDInsight в наборе средств Azure для IntelliJ для отправки задания Spark в кластер HDInsight Spark и его удаленной отладки с настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="127a8-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="127a8-107">Для этого необходимо выполнить перечисленные ниже общие шаги.</span><span class="sxs-lookup"><span data-stu-id="127a8-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="127a8-108">Создание виртуальной сети Azure типа "сеть — сеть" или "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="127a8-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="127a8-109">В инструкциях в этом документе предполагается, что вы используете тип "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="127a8-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="127a8-110">Создание в Azure HDInsight кластера Spark, который является частью виртуальной сети Azure типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="127a8-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="127a8-111">Проверка подключения между головным узлом кластера и компьютером.</span><span class="sxs-lookup"><span data-stu-id="127a8-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="127a8-112">Создание приложения Scala в IntelliJ IDEA и его настройка для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="127a8-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="127a8-113">Запуск и отладка приложения.</span><span class="sxs-lookup"><span data-stu-id="127a8-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="127a8-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="127a8-114">Prerequisites</span></span>
* <span data-ttu-id="127a8-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="127a8-115">An Azure subscription.</span></span> <span data-ttu-id="127a8-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="127a8-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="127a8-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="127a8-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="127a8-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="127a8-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="127a8-119">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="127a8-119">Oracle Java Development kit.</span></span> <span data-ttu-id="127a8-120">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="127a8-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="127a8-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="127a8-121">IntelliJ IDEA.</span></span> <span data-ttu-id="127a8-122">В этой статье используется версия 2017.1.</span><span class="sxs-lookup"><span data-stu-id="127a8-122">This article uses version 2017.1.</span></span> <span data-ttu-id="127a8-123">Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="127a8-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="127a8-124">Средства HDInsight в наборе средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="127a8-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="127a8-125">Средства HDInsight для IntelliJ доступны в составе набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="127a8-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="127a8-126">Инструкции по установке набора средств Azure см. в статье [Установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="127a8-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="127a8-127">Войдите в подписку Azure из IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="127a8-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="127a8-128">Следуйте указаниям, приведенным [здесь](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="127a8-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="127a8-129">При запуске приложения Spark Scala для удаленной отладки на компьютере Windows может возникнуть исключение, описанное в [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) и связанное с отсутствием в Windows файла WinUtils.exe.</span><span class="sxs-lookup"><span data-stu-id="127a8-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="127a8-130">Чтобы обойти эту ошибку, [скачайте этот исполняемый файл отсюда](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe), например в папку **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="127a8-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="127a8-131">После этого добавьте переменную среды **HADOOP_HOME** и присвойте ей значение **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="127a8-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="127a8-132">Шаг 1. Создание виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="127a8-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="127a8-133">Следуйте инструкциям по созданию виртуальной сети Azure по ссылкам ниже. Затем проверьте сетевое подключение между своим компьютером и виртуальной сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="127a8-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="127a8-134">Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="127a8-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="127a8-135">Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="127a8-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="127a8-136">Настройка подключения к виртуальной сети типа "точка — сеть" с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="127a8-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="127a8-137">Шаг 2. Создание кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="127a8-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="127a8-138">Кроме того, следует создать в Azure HDInsight кластер Apache Spark в составе созданной вами виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="127a8-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="127a8-139">Воспользуйтесь сведениями из статьи [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="127a8-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="127a8-140">На этапе дополнительной настройки выберите виртуальную сеть Azure, созданную на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="127a8-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="127a8-141">Шаг 3. Проверка сетевого подключения между головным узлом кластера и компьютером</span><span class="sxs-lookup"><span data-stu-id="127a8-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="127a8-142">Прежде всего необходимо получить IP-адрес головного узла.</span><span class="sxs-lookup"><span data-stu-id="127a8-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="127a8-143">Откройте пользовательский интерфейс Ambari для кластера.</span><span class="sxs-lookup"><span data-stu-id="127a8-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="127a8-144">В колонке кластера щелкните **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="127a8-144">From the cluster blade, click **Dashboard**.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="127a8-146">В правом верхнем углу окна пользовательского интерфейса Ambari щелкните **Узлы**.</span><span class="sxs-lookup"><span data-stu-id="127a8-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="127a8-148">Отобразится список головных узлов, рабочих узлов и узлов zookeeper.</span><span class="sxs-lookup"><span data-stu-id="127a8-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="127a8-149">Головные узлы обозначены префиксом **hn***.</span><span class="sxs-lookup"><span data-stu-id="127a8-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="127a8-150">Щелкните первый головной узел.</span><span class="sxs-lookup"><span data-stu-id="127a8-150">Click the first headnode.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="127a8-152">В нижней части открывшейся страницы скопируйте IP-адрес и имя головного узла в поле **Сводка** .</span><span class="sxs-lookup"><span data-stu-id="127a8-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="127a8-154">Добавьте IP-адрес и имя головного узла в файл **Узлы** на компьютере, с которого собираетесь выполнять и удаленно отлаживать задания Spark.</span><span class="sxs-lookup"><span data-stu-id="127a8-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="127a8-155">Это обеспечит обмен данными с головным узлом.</span><span class="sxs-lookup"><span data-stu-id="127a8-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="127a8-156">Откройте блокнот с повышенным уровнем разрешений.</span><span class="sxs-lookup"><span data-stu-id="127a8-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="127a8-157">В меню "Файл" выберите пункт **Открыть** и перейдите в папку с файлом hosts.</span><span class="sxs-lookup"><span data-stu-id="127a8-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="127a8-158">На компьютере под управлением Windows это папка `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="127a8-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="127a8-159">Добавьте в файл **hosts** указанные далее данные.</span><span class="sxs-lookup"><span data-stu-id="127a8-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="127a8-160">С компьютера, подключенного к виртуальной сети Azure и использующегося кластером HDInsight, проверьте связь с обоими головными узлами при помощи IP-адреса и имени узла.</span><span class="sxs-lookup"><span data-stu-id="127a8-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="127a8-161">Установите SSH-подключение к головному узлу кластера, воспользовавшись инструкциями из раздела [Подключение к кластеру HDInsight на основе Linux](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="127a8-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="127a8-162">Проверьте связь головного узла кластера с компьютером при помощь IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="127a8-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="127a8-163">Следует проверить возможность подключения к обоим IP-адресам, назначенным компьютеру. Один предназначен для сетевого подключения, а другой — для виртуальной сети Azure, к которой подключен компьютер.</span><span class="sxs-lookup"><span data-stu-id="127a8-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="127a8-164">Повторите эти действия на другом головном узле.</span><span class="sxs-lookup"><span data-stu-id="127a8-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="127a8-165">Шаг 4. Создание приложения Spark Scala при помощи средств HDInsight в наборе средств Azure для IntelliJ и его настройка для удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="127a8-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="127a8-166">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="127a8-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="127a8-167">В диалоговом окне нового проекта установите параметры, как на снимке экрана ниже, а затем нажмите кнопку **Next**(«Далее»).</span><span class="sxs-lookup"><span data-stu-id="127a8-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="127a8-169">В левой области выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="127a8-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="127a8-170">В правой области выберите **Spark on HDInsight (Scala)**(Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="127a8-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="127a8-171">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="127a8-171">Click **Next**.</span></span>
2. <span data-ttu-id="127a8-172">В следующем окне укажите приведенные ниже сведения, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="127a8-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="127a8-173">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="127a8-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="127a8-174">Для параметра **Project SDK** (Пакет SDK проекта) выберите Java 1.8 для кластера Spark 2.x или Java 1.7 для кластера Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="127a8-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="127a8-175">Для параметра **Spark Version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK Spark и пакета SDK Scala.</span><span class="sxs-lookup"><span data-stu-id="127a8-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="127a8-176">Если версия кластера Spark ниже, чем 2.0, выберите Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="127a8-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="127a8-177">В противном случае следует выбрать Spark 2.x.</span><span class="sxs-lookup"><span data-stu-id="127a8-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="127a8-178">В этом примере используется Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="127a8-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="127a8-179">![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="127a8-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="127a8-180">Проект Spark автоматически создаст артефакт.</span><span class="sxs-lookup"><span data-stu-id="127a8-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="127a8-181">Чтобы просмотреть артефакт, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="127a8-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="127a8-182">В меню **File** (Файл) выберите пункт **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="127a8-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="127a8-183">В диалоговом окне **Project Structure** (Структура проекта) щелкните **Артефакты**, чтобы просмотреть созданный по умолчанию артефакт.</span><span class="sxs-lookup"><span data-stu-id="127a8-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="127a8-184">![Создание JAR-файла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="127a8-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="127a8-185">Кроме того, можно создать свой собственный артефакт, щелкнув значок **+** , выделенный на рисунке выше.</span><span class="sxs-lookup"><span data-stu-id="127a8-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="127a8-186">Добавьте библиотеки в проект.</span><span class="sxs-lookup"><span data-stu-id="127a8-186">Add libraries to your project.</span></span> <span data-ttu-id="127a8-187">Чтобы добавить библиотеку, щелкните правой кнопкой мыши имя проекта в дереве проектов и выберите пункт **Open Module Settings**(Открыть параметры модуля).</span><span class="sxs-lookup"><span data-stu-id="127a8-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="127a8-188">В левой области диалогового окна **Project Structure** (Структура проекта) выберите пункт **Библиотеки**, щелкните знак (+) и выберите пункт **From Maven** (Из Maven).</span><span class="sxs-lookup"><span data-stu-id="127a8-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![Добавление библиотеки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="127a8-190">В диалоговом окне **Download Library from Maven Repository** (Скачивание библиотеки из репозитория Maven) найдите и добавьте перечисленные ниже библиотеки.</span><span class="sxs-lookup"><span data-stu-id="127a8-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="127a8-191">Скопируйте файлы `yarn-site.xml` и `core-site.xml` с головного узла кластера и добавьте их в проект.</span><span class="sxs-lookup"><span data-stu-id="127a8-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="127a8-192">Выполните указанные ниже команды, чтобы скопировать файлы.</span><span class="sxs-lookup"><span data-stu-id="127a8-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="127a8-193">Для выполнения приведенных далее команд `scp` можно использовать [Cygwin](https://cygwin.com/install.html). Это позволит копировать файлы из головных узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="127a8-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="127a8-194">Так как мы уже добавили IP-адреса и имена головных узлов кластера в файл hosts на компьютере, можно использовать команды **scp** , как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="127a8-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="127a8-195">Добавьте эти файлы в проект, скопировав их в папку **/src** дерева проектов, например `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="127a8-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="127a8-196">Обновите `core-site.xml` , чтобы внести описанные ниже изменения.</span><span class="sxs-lookup"><span data-stu-id="127a8-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="127a8-197">`core-site.xml` содержит зашифрованный ключ учетной записи хранения, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="127a8-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="127a8-198">В файле `core-site.xml` , добавленном в проект, замените зашифрованный ключ фактическим ключом к хранилищу данных, связанным с учетной записью хранения, используемой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="127a8-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="127a8-199">Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="127a8-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="127a8-200">Удалите из файла `core-site.xml`указанные ниже записи.</span><span class="sxs-lookup"><span data-stu-id="127a8-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="127a8-201">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="127a8-201">Save the file.</span></span>
7. <span data-ttu-id="127a8-202">Добавьте класс Main для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="127a8-202">Add the Main class for your application.</span></span> <span data-ttu-id="127a8-203">В **обозревателе проектов** щелкните правой кнопкой мыши **src**, наведите указатель мыши на пункт **Создать** и щелкните **Scala Class** (Класс Scala).</span><span class="sxs-lookup"><span data-stu-id="127a8-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="127a8-205">В диалоговом окне **Create New Scala Class** (Создание класса Scala) введите имя, в поле **Вид** выберите **Объект** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="127a8-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="127a8-207">Скопируйте приведенный ниже код и вставьте его в файл `MyClusterAppMain.scala` .</span><span class="sxs-lookup"><span data-stu-id="127a8-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="127a8-208">Этот код создает контекст Spark и запускает метод `executeJob` из объекта `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="127a8-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="127a8-209">Повторите шаги 8 и 9, описанные выше, чтобы добавить новый объект Scala с именем `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="127a8-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="127a8-210">Добавьте в этот класс приведенный далее код.</span><span class="sxs-lookup"><span data-stu-id="127a8-210">To this class add the following code.</span></span> <span data-ttu-id="127a8-211">Этот код считывает данные из файла HVAC.csv (доступного для всех кластеров HDInsight Spark), извлекает строки, содержащие только одну цифру в седьмом столбце CSV-файла, и записывает результат в **/HVACOut** в используемом по умолчанию контейнере хранилища для кластера.</span><span class="sxs-lookup"><span data-stu-id="127a8-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="127a8-212">Повторите шаги 8 и 9, описанные выше, чтобы добавить новый класс с именем `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="127a8-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="127a8-213">Этот класс реализует платформу тестирования Spark, которая используется для отладки приложений.</span><span class="sxs-lookup"><span data-stu-id="127a8-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="127a8-214">Добавьте в класс `RemoteClusterDebugging` приведенный далее код.</span><span class="sxs-lookup"><span data-stu-id="127a8-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="127a8-215">При этом необходимо обратить внимание на несколько важных моментов.</span><span class="sxs-lookup"><span data-stu-id="127a8-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="127a8-216">Для `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`убедитесь, что JAR-файл сборки Spark доступен в хранилище кластера по указанному пути.</span><span class="sxs-lookup"><span data-stu-id="127a8-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="127a8-217">Для `setJars`укажите расположение, где будет создан JAR-файл артефакта.</span><span class="sxs-lookup"><span data-stu-id="127a8-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="127a8-218">Обычно это `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="127a8-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="127a8-219">В классе `RemoteClusterDebugging` щелкните правой кнопкой мыши ключевое слово `test` и выберите пункт **Create RemoteClusterDebugging Configuration** (Создать конфигурацию RemoteClusterDebugging).</span><span class="sxs-lookup"><span data-stu-id="127a8-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="127a8-221">В диалоговом окне введите имя конфигурации и выберите для параметра **Test kind** (Тип теста) значение **Имя теста**.</span><span class="sxs-lookup"><span data-stu-id="127a8-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="127a8-222">Оставьте остальные значения, установленные по умолчанию, нажмите кнопку **Применить**, а затем — кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="127a8-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="127a8-224">В строке меню должен отобразиться раскрывающийся список конфигурации **Remote Run** (Удаленный запуск).</span><span class="sxs-lookup"><span data-stu-id="127a8-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="127a8-226">Шаг 5. Запуск приложения в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="127a8-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="127a8-227">В проекте IntelliJ IDEA откройте `SparkSample.scala` и создайте точку останова рядом с "val rdd1".</span><span class="sxs-lookup"><span data-stu-id="127a8-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="127a8-228">В контекстном меню создания точки останова выберите пункт **line in function executeJob**(Строка функции executeJob).</span><span class="sxs-lookup"><span data-stu-id="127a8-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Добавление точки останова](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="127a8-230">Нажмите кнопку **Debug Run** (Запуск отладки) рядом с раскрывающимся списком конфигурации **Удаленный запуск**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="127a8-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="127a8-232">Когда выполнение программы достигнет точки останова, на нижней панели отобразится вкладка **Debugger** (Отладчик).</span><span class="sxs-lookup"><span data-stu-id="127a8-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="127a8-234">Щелкните значок (**+**), чтобы добавить контрольное значение, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="127a8-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="127a8-236">В данном случае, так как приложение было остановлено до создания переменной `rdd1`, при помощи этого контрольного значения можно увидеть первые пять строк для переменной `rdd`.</span><span class="sxs-lookup"><span data-stu-id="127a8-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="127a8-237">Нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="127a8-237">Press **ENTER**.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="127a8-239">Как видно на рисунке выше, во время выполнения можно создавать запросы на терабайты данных и отлаживать работу приложения.</span><span class="sxs-lookup"><span data-stu-id="127a8-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="127a8-240">Например, в результатах на рисунке выше можно увидеть, что первая строка выходных данных является заголовком.</span><span class="sxs-lookup"><span data-stu-id="127a8-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="127a8-241">На основе этих данных можно изменить код приложения, если требуется пропустить строку заголовка.</span><span class="sxs-lookup"><span data-stu-id="127a8-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="127a8-242">Теперь можно щелкнуть значок **Resume Program** (Возобновить работу программы), чтобы продолжить выполнение приложения.</span><span class="sxs-lookup"><span data-stu-id="127a8-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="127a8-244">Если работа приложения завершится успешно, отобразится результат, подобный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="127a8-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![Запуск программы в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="127a8-246"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="127a8-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="127a8-247">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="127a8-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="127a8-248">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="127a8-248">Demo</span></span>
* <span data-ttu-id="127a8-249">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="127a8-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="127a8-250">Удаленная отладка (видео): [удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="127a8-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="127a8-251">Сценарии</span><span class="sxs-lookup"><span data-stu-id="127a8-251">Scenarios</span></span>
* [<span data-ttu-id="127a8-252">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="127a8-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="127a8-253">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="127a8-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="127a8-254">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="127a8-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="127a8-255">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="127a8-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="127a8-256">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="127a8-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="127a8-257">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="127a8-257">Create and run applications</span></span>
* [<span data-ttu-id="127a8-258">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="127a8-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="127a8-259">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="127a8-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="127a8-260">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="127a8-260">Tools and extensions</span></span>
* [<span data-ttu-id="127a8-261">Использование средств HDInsight в наборе средств Azure для IntelliJ для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="127a8-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="127a8-262">Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="127a8-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="127a8-263">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="127a8-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="127a8-264">Использование средств HDInsight в наборе средств Azure для Eclipse для создания приложений Spark</span><span class="sxs-lookup"><span data-stu-id="127a8-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="127a8-265">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="127a8-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="127a8-266">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="127a8-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="127a8-267">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="127a8-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="127a8-268">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="127a8-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="127a8-269">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="127a8-269">Manage resources</span></span>
* [<span data-ttu-id="127a8-270">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="127a8-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="127a8-271">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="127a8-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
