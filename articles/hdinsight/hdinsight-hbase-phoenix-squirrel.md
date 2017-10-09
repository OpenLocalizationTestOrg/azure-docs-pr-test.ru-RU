---
title: "aaaUse Финиксе Apache и белка с ОС Windows Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Финиксе Apache в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="b1466-103">Использование Apache Phoenix и SQuirreL с кластерами HBase под управлением Windows в HDinsight</span><span class="sxs-lookup"><span data-stu-id="b1466-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="b1466-104">Узнайте, как toouse [Финиксе Apache](http://phoenix.apache.org/) в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1466-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="b1466-105">Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше).</span><span class="sxs-lookup"><span data-stu-id="b1466-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="b1466-106">Hello Финиксе грамматики. в разделе [грамматики Финиксе](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="b1466-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="b1466-107">Hello Финиксе сведения о версии в HDInsight, в разделе [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b1466-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="b1466-108">Hello шагов в работают только этот документ для кластеров HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="b1466-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b1466-109">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="b1466-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="b1466-110">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b1466-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b1466-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b1466-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="b1466-112">Сведения об использовании Phoenix в HDInsight под управлением Linux см. в статье [Использование Apache Phoenix с кластерами HBase под управлением Linux в HDinsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b1466-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="b1466-113">Использование SQLLine</span><span class="sxs-lookup"><span data-stu-id="b1466-113">Use SQLLine</span></span>
<span data-ttu-id="b1466-114">[SQLLine](http://sqlline.sourceforge.net/) является tooexecute служебной программы командной строки SQL.</span><span class="sxs-lookup"><span data-stu-id="b1466-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b1466-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1466-115">Prerequisites</span></span>
<span data-ttu-id="b1466-116">Прежде чем использовать SQLLine, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="b1466-117">**Кластер HBase в HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="b1466-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="b1466-118">Сведения о подготовке кластера HBase см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="b1466-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="b1466-119">**Подключите кластер HBase toohello посредством протокола удаленного рабочего стола hello**.</span><span class="sxs-lookup"><span data-stu-id="b1466-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="b1466-120">Инструкции см. в разделе [кластеров управление Hadoop в HDInsight с помощью классического портала Azure hello][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="b1466-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="b1466-121">**toofind hello имени узла**</span><span class="sxs-lookup"><span data-stu-id="b1466-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="b1466-122">Откройте **командной строки Hadoop** с рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="b1466-123">Выполните следующие команды tooget hello DNS-суффикс hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="b1466-124">Запишите **DNS-суффикс, зависящий от подключения**.</span><span class="sxs-lookup"><span data-stu-id="b1466-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="b1466-125">Например, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="b1466-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="b1466-126">При подключении tooan HBase кластера, необходимо будет tooone tooconnect из Zookeepers hello, используя полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="b1466-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="b1466-127">Каждый кластер HDInsight содержит 3 Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="b1466-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="b1466-128">Их имена — *zookeeper0*, *zookeeper1* и *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="b1466-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="b1466-129">Hello полное доменное имя будет примерно *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="b1466-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="b1466-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="b1466-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="b1466-131">Откройте **командной строки Hadoop** с рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="b1466-132">Выполните следующие команды tooopen SQLLine hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="b1466-134">Hello команды, используемые в образце hello:</span><span class="sxs-lookup"><span data-stu-id="b1466-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="b1466-135">Дополнительные сведения см. в разделе [SQLLine manual](http://sqlline.sourceforge.net/#manual) (Руководство по SQLLine) и [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).</span><span class="sxs-lookup"><span data-stu-id="b1466-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="b1466-136">Использование SQuirreL</span><span class="sxs-lookup"><span data-stu-id="b1466-136">Use SQuirreL</span></span>
<span data-ttu-id="b1466-137">[Клиент SQL белка](http://squirrel-sql.sourceforge.net/) — это графическая программа Java, позволяют tooview структура hello JDBC совместимую базу данных, Обзор hello данные в таблицах, команд SQL и т. д. Это может быть tooApache используется tooconnect Финиксе на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1466-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="b1466-138">В этом разделе показано, как tooinstall и настройте белка на рабочей станции tooconnect tooan HBase кластера в HDInsight через VPN.</span><span class="sxs-lookup"><span data-stu-id="b1466-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b1466-139">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1466-139">Prerequisites</span></span>
<span data-ttu-id="b1466-140">Перед выполнением процедуры hello, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="b1466-141">Кластер HBase развернуть tooan виртуальную сеть Azure с виртуальной машины DNS.</span><span class="sxs-lookup"><span data-stu-id="b1466-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="b1466-142">Инструкции см. в статье [Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="b1466-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="b1466-143">Получение hello HBase кластера кластера DNS подключения-суффикс.</span><span class="sxs-lookup"><span data-stu-id="b1466-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="b1466-144">tooget его RDP в кластер hello, а затем выполните команду IPConfig.</span><span class="sxs-lookup"><span data-stu-id="b1466-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="b1466-145">DNS-суффикс Hello похожа на:</span><span class="sxs-lookup"><span data-stu-id="b1466-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="b1466-146">Скачать и установить [Microsoft Visual Studio Express для Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) на рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="b1466-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="b1466-147">Необходимо будет makecert из пакета toocreate hello свой сертификат.</span><span class="sxs-lookup"><span data-stu-id="b1466-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="b1466-148">Загрузить и установить среду [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) на рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="b1466-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="b1466-149">Для SQL-клиента SQuirreL версии 3.0 и выше требуется JRE версии 1.6 или выше.</span><span class="sxs-lookup"><span data-stu-id="b1466-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="b1466-150">Настройка toohello подключение точка-сеть VPN виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="b1466-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="b1466-151">Настройка VPN-подключения «точка-сайт» предусматривает 3 шага:</span><span class="sxs-lookup"><span data-stu-id="b1466-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="b1466-152">Настройка виртуальной сети и шлюза динамической маршрутизации</span><span class="sxs-lookup"><span data-stu-id="b1466-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="b1466-153">Создание сертификатов</span><span class="sxs-lookup"><span data-stu-id="b1466-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="b1466-154">Настройка VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="b1466-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="b1466-155">В разделе [Настройка tooan подключение точка-сеть VPN виртуальной сети Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="b1466-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="b1466-156">Настройка виртуальной сети и шлюза динамической маршрутизации</span><span class="sxs-lookup"><span data-stu-id="b1466-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="b1466-157">Обеспечить вы подготовили кластер HBase в виртуальной сети Azure (см. предварительные требования hello для этого раздела).</span><span class="sxs-lookup"><span data-stu-id="b1466-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="b1466-158">Hello следующим шагом является tooconfigure подключение точка сеть.</span><span class="sxs-lookup"><span data-stu-id="b1466-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="b1466-159">**подключение точка сеть tooconfigure hello**</span><span class="sxs-lookup"><span data-stu-id="b1466-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="b1466-160">Войдите в toohello [классический портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b1466-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="b1466-161">В левой части экрана приветствия щелкните **СЕТЕЙ**.</span><span class="sxs-lookup"><span data-stu-id="b1466-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="b1466-162">Нажмите кнопку создания виртуальной сети hello (см. [HBase подготовки кластеров в виртуальной сети Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="b1466-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="b1466-163">Нажмите кнопку **Настройка** сверху hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="b1466-164">В hello **подключение точка сеть** выберите **Настройка подключения «точка сеть»**.</span><span class="sxs-lookup"><span data-stu-id="b1466-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="b1466-165">Настройка **НАЧАЛЬНЫЙ IP-адрес** и **CIDR** адрес toospecify hello IP-адресов из которого клиенты VPN будут получать IP-адрес при подключении.</span><span class="sxs-lookup"><span data-stu-id="b1466-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="b1466-166">Hello диапазон не пересекается с другими hello диапазонами, выделенными в локальной сети и hello виртуальной сети Azure, вы будете подключаться.</span><span class="sxs-lookup"><span data-stu-id="b1466-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="b1466-167">Например, если выбран диапазон 10.0.0.0/20 для виртуальной сети, для пространства клиентских адресов можно выбрать 10.1.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="b1466-167">For example.</span></span> <span data-ttu-id="b1466-168">Если вы выбрали 10.0.0.0/20 для hello виртуальной сети, можно выбрать 10.1.0.0/24 hello клиента адресного пространства.</span><span class="sxs-lookup"><span data-stu-id="b1466-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="b1466-169">В разделе hello [точка-сеть] [ vnet-point-to-site-connectivity] более подробную информацию.</span><span class="sxs-lookup"><span data-stu-id="b1466-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="b1466-170">В разделе пространства адресов виртуальной сети hello, нажмите кнопку **добавить подсеть шлюза**.</span><span class="sxs-lookup"><span data-stu-id="b1466-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="b1466-171">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="b1466-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="b1466-172">Нажмите кнопку **Да** tooconfirm hello изменений.</span><span class="sxs-lookup"><span data-stu-id="b1466-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="b1466-173">Дождитесь завершения внесения изменения перед выполнением следующей процедуры toohello hello hello системой.</span><span class="sxs-lookup"><span data-stu-id="b1466-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="b1466-174">**toocreate шлюз динамической маршрутизации**</span><span class="sxs-lookup"><span data-stu-id="b1466-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="b1466-175">Hello классический портал Azure, щелкните **МОНИТОРИНГА** из hello вверху страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="b1466-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="b1466-176">Нажмите кнопку **создать ШЛЮЗ** из hello внизу страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="b1466-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="b1466-177">Нажмите кнопку **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="b1466-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="b1466-178">Подождите, пока создается hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="b1466-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="b1466-179">Нажмите кнопку **МОНИТОРИНГА** сверху hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="b1466-180">Вы увидите графическую диаграмму hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b1466-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Схема виртуальной сети Azure «точка-сайт»][img-vnet-diagram]

    <span data-ttu-id="b1466-182">Hello показан 0 клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="b1466-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="b1466-183">После внесения toohello подключения виртуальной сети, число hello будет обновленные tooone.</span><span class="sxs-lookup"><span data-stu-id="b1466-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="b1466-184">Создание сертификатов</span><span class="sxs-lookup"><span data-stu-id="b1466-184">Create your certificates</span></span>
<span data-ttu-id="b1466-185">Одним из способов toocreate — сертификат X.509 с помощью hello средство создания сертификатов (makecert.exe), входящая в состав [Microsoft Visual Studio Express для Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1466-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="b1466-186">**toocreate самозаверяющий корневой сертификат**</span><span class="sxs-lookup"><span data-stu-id="b1466-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="b1466-187">На рабочей станции откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="b1466-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="b1466-188">Перейдите в папку средств Visual Studio toohello.</span><span class="sxs-lookup"><span data-stu-id="b1466-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="b1466-189">следующую команду в следующем примере hello Hello создать и установить корневой сертификат в хранилище личных сертификатов hello на рабочей станции и также создать соответствующий CER-файл, который позднее будет отправлен toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1466-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="b1466-190">Изменение каталога toohello нужного hello, расположенных в, где требуется toouse для hello сертификата имя hello HBaseVnetVPNRootCertificate toobe файл .cer.</span><span class="sxs-lookup"><span data-stu-id="b1466-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="b1466-191">Не закрывайте окно командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="b1466-192">Он понадобится в следующей процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b1466-193">Поскольку был создан корневой сертификат, из которого будут создаваться сертификаты клиента, можно tooexport этот сертификат и его закрытый ключ и сохраните его в безопасном месте tooa, откуда его можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="b1466-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="b1466-194">**toocreate сертификат клиента**</span><span class="sxs-lookup"><span data-stu-id="b1466-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="b1466-195">Из hello же командную строку (он имеет toobe на hello же компьютере, где была создана hello корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="b1466-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="b1466-196">Hello сертификат клиента должен быть создан из hello корневого сертификата), выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b1466-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="b1466-197">HBaseVnetVPNRootCertificate — имя сертификата корневого hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="b1466-198">Он имеет имя toomatch hello корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="b1466-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="b1466-199">Hello корневой сертификат и сертификат клиента hello хранятся в хранилище личных сертификатов на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b1466-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="b1466-200">Используйте certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="b1466-200">Use certmgr.msc tooverify.</span></span>

    ![Схема виртуальной сети Azure "точка — сеть"][img-certificate]

    <span data-ttu-id="b1466-202">Сертификат клиента должны устанавливаться на каждом компьютере, что требуется tooconnect toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b1466-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="b1466-203">Рекомендуется создавать уникальные клиентские сертификаты для каждого компьютера, которые должны tooconnect toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b1466-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="b1466-204">tooexport hello клиентских сертификатов, используйте certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="b1466-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="b1466-205">**tooupload hello корневой сертификат toohello классический портал Azure**</span><span class="sxs-lookup"><span data-stu-id="b1466-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="b1466-206">Hello классический портал Azure, щелкните **сети** hello левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="b1466-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="b1466-207">Щелкните hello виртуальной сети, где развертывается кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="b1466-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="b1466-208">Нажмите кнопку **СЕРТИФИКАТЫ** сверху hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="b1466-209">Нажмите кнопку **отправить** из hello вниз и укажите файл корневого сертификата hello, созданную в процедуре hello перед последней.</span><span class="sxs-lookup"><span data-stu-id="b1466-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="b1466-210">Подождите, пока сертификат hello импортированы.</span><span class="sxs-lookup"><span data-stu-id="b1466-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="b1466-211">Нажмите кнопку **МОНИТОРИНГА** hello верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b1466-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="b1466-212">Hello виртуального диаграмма показывает состояние hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="b1466-213">Настройка VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="b1466-213">Configure your VPN client</span></span>
<span data-ttu-id="b1466-214">**toodownload и установите пакет клиента VPN hello**</span><span class="sxs-lookup"><span data-stu-id="b1466-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="b1466-215">На странице панели МОНИТОРИНГА hello hello виртуальной сети, в разделе "быстрый обзор" hello щелкните **загрузки hello пакет VPN-клиента для 64-разрядных** или **загрузки hello пакет клиента VPN 32-разрядных** на основе вашего версия операционной системы рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="b1466-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="b1466-216">Нажмите кнопку **запуска** tooinstall hello пакета.</span><span class="sxs-lookup"><span data-stu-id="b1466-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="b1466-217">В строке приветствия безопасности, нажмите кнопку **Подробнее**и нажмите кнопку **выполнения изменение**.</span><span class="sxs-lookup"><span data-stu-id="b1466-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="b1466-218">Нажмите кнопку **Да** дважды.</span><span class="sxs-lookup"><span data-stu-id="b1466-218">Click **Yes** twice.</span></span>

<span data-ttu-id="b1466-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="b1466-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="b1466-220">На рабочем столе hello рабочей станции щелкните значок сети hello hello панели задач.</span><span class="sxs-lookup"><span data-stu-id="b1466-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="b1466-221">Должно отобразиться VPN-подключения с именем вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b1466-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="b1466-222">Щелкните имя подключения VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="b1466-223">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b1466-223">Click **Connect**.</span></span>

<span data-ttu-id="b1466-224">**hello tootest подключение VPN, разрешения имен при домена**</span><span class="sxs-lookup"><span data-stu-id="b1466-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="b1466-225">Hello рабочей станции, откройте командную строку и ping один hello следующие имена приведенные hello HBase кластера DNS-суффикс — myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="b1466-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="b1466-226">Установка и настройка SQuirreL на рабочей станции</span><span class="sxs-lookup"><span data-stu-id="b1466-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="b1466-227">**tooinstall белка**</span><span class="sxs-lookup"><span data-stu-id="b1466-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="b1466-228">Загрузите hello клиента белка SQL jar-файл из [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="b1466-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="b1466-229">Открытие и запуск hello jar-файл.</span><span class="sxs-lookup"><span data-stu-id="b1466-229">Open/run hello jar file.</span></span> <span data-ttu-id="b1466-230">Он требует hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="b1466-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="b1466-231">Нажмите кнопку **Далее** дважды.</span><span class="sxs-lookup"><span data-stu-id="b1466-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="b1466-232">Укажите путь к которому у вас есть hello разрешение на запись и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b1466-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b1466-233">устанавливается в папку по умолчанию Hello в папке C:\Program Files\squirrel-sql-3.6 hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="b1466-234">Путь toothis toowrite заказа установщик hello должны быть предоставлены права администратора hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="b1466-235">Откройте командную строку от имени администратора, перейдите в папку bin в tooJava и затем запустите:</span><span class="sxs-lookup"><span data-stu-id="b1466-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="b1466-236">Java.exe-jar [hello путь hello белка jar-файл]</span><span class="sxs-lookup"><span data-stu-id="b1466-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="b1466-237">Нажмите кнопку **ОК** tooconfirm Создание hello целевой каталог.</span><span class="sxs-lookup"><span data-stu-id="b1466-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="b1466-238">по умолчанию Hello — tooinstall hello базы и стандартных пакетов.</span><span class="sxs-lookup"><span data-stu-id="b1466-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="b1466-239">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b1466-239">Click **Next**.</span></span>
7. <span data-ttu-id="b1466-240">Нажмите кнопку **Далее** дважды, а затем нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b1466-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="b1466-241">**драйвер Финиксе tooinstall hello**</span><span class="sxs-lookup"><span data-stu-id="b1466-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="b1466-242">Hello Финиксе драйвер jar-файл находится на кластер HBase hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="b1466-243">путь Hello — примерно следующее toohello, основанных на версиях hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="b1466-244">Требуется toocopy его tooyour рабочей станции под hello [папка установки белка] / lib пути.</span><span class="sxs-lookup"><span data-stu-id="b1466-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="b1466-245">Hello простым способом является tooRDP в hello кластера, а затем используйте файл копирования и вставки (CTRL + C и CTRL + V) toocopy его tooyour рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="b1466-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="b1466-246">**tooadd tooSQuirreL драйвер Phoenix**</span><span class="sxs-lookup"><span data-stu-id="b1466-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="b1466-247">Откройте SQL-клиент SQuirreL на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="b1466-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="b1466-248">Нажмите кнопку hello **драйвер** вкладке слева hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="b1466-249">Из hello **драйверы** меню, нажмите кнопку **новый драйвер**.</span><span class="sxs-lookup"><span data-stu-id="b1466-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="b1466-250">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="b1466-250">Enter hello following information:</span></span>

   * <span data-ttu-id="b1466-251">**Имя**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="b1466-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="b1466-252">**Пример URL-адреса**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b1466-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="b1466-253">**Имя класса**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="b1466-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="b1466-254">Пользователь все нижнего регистра в hello пример URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="b1466-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="b1466-255">Можно использовать весь набор zookeeper в случае, если один из них не работает.</span><span class="sxs-lookup"><span data-stu-id="b1466-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="b1466-256">имена узлов Hello: zookeeper0, zookeeper1 и zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="b1466-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Драйвер HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. <span data-ttu-id="b1466-258">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1466-258">Click **OK**.</span></span>

<span data-ttu-id="b1466-259">**toocreate кластер HBase toohello псевдоним**</span><span class="sxs-lookup"><span data-stu-id="b1466-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="b1466-260">Щелкните hello белка, **псевдонимы** вкладке слева hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="b1466-261">Из hello **псевдонимы** меню, нажмите кнопку **новый псевдоним**.</span><span class="sxs-lookup"><span data-stu-id="b1466-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="b1466-262">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="b1466-262">Enter hello following information:</span></span>

   * <span data-ttu-id="b1466-263">**Имя**: hello имя кластера HBase hello или любое имя, вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="b1466-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="b1466-264">**Драйвер**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="b1466-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="b1466-265">Это должно соответствовать имени драйвера hello, созданный в последней процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="b1466-266">**URL-адрес**: hello, URL-адрес копируется из конфигурации драйвера.</span><span class="sxs-lookup"><span data-stu-id="b1466-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="b1466-267">Убедитесь, что toouser все строчные.</span><span class="sxs-lookup"><span data-stu-id="b1466-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="b1466-268">**Имя пользователя**: может быть любой текстовой строкой.</span><span class="sxs-lookup"><span data-stu-id="b1466-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="b1466-269">Поскольку здесь использовать VPN-подключение имя пользователя hello вообще не используется.</span><span class="sxs-lookup"><span data-stu-id="b1466-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="b1466-270">**Пароль**: может быть любой текстовой строкой.</span><span class="sxs-lookup"><span data-stu-id="b1466-270">**Password**: It can be any text.</span></span>

     ![Драйвер HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. <span data-ttu-id="b1466-272">Нажмите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="b1466-272">Click **Test**.</span></span>
5. <span data-ttu-id="b1466-273">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b1466-273">Click **Connect**.</span></span> <span data-ttu-id="b1466-274">Когда он создает соединение hello белка выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b1466-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="b1466-276">**toorun теста**</span><span class="sxs-lookup"><span data-stu-id="b1466-276">**toorun a test**</span></span>

1. <span data-ttu-id="b1466-277">Нажмите кнопку hello **SQL** вкладки справа Далее toohello **объектов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b1466-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="b1466-278">Скопируйте и вставьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="b1466-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="b1466-279">Нажмите кнопку выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="b1466-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="b1466-281">Перейдите назад toohello **объектов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b1466-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="b1466-282">Разверните имя псевдонима hello, а затем разверните **таблицы**.</span><span class="sxs-lookup"><span data-stu-id="b1466-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="b1466-283">Вы увидите новую таблицу hello, перечисленных в разделе.</span><span class="sxs-lookup"><span data-stu-id="b1466-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1466-284">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1466-284">Next steps</span></span>
<span data-ttu-id="b1466-285">В этой статье вы узнали как toouse Финиксе Apache в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1466-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="b1466-286">toolearn более, см.</span><span class="sxs-lookup"><span data-stu-id="b1466-286">toolearn more, see</span></span>

* <span data-ttu-id="b1466-287">[Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="b1466-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="b1466-288">[Подготовка кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]: С интеграцией виртуальной сети кластеров HBase может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую.</span><span class="sxs-lookup"><span data-stu-id="b1466-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="b1466-289">[Настройка репликации HBase HDInsight](hdinsight-hbase-replication.md): Узнайте, как tooconfigure HBase репликации между двумя центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b1466-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="b1466-290">[Анализ мнений Twitter с HBase в HDInsight][hbase-twitter-sentiment]: Узнайте, как toodo в режиме реального времени [анализ мнений](http://en.wikipedia.org/wiki/Sentiment_analysis) больших данных с помощью кластера Hadoop в HDInsight HBase.</span><span class="sxs-lookup"><span data-stu-id="b1466-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
