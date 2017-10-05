---
title: "Установка Presto в кластерах Azure HDInsight на платформе Linux | Документация Майкрософт"
description: "Узнайте, как устанавливать Presto и Airpal в кластерах HDInsight Hadoop на основе Linux с помощью действий сценария."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="e9bda-103">Установка и использование Presto в кластерах HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="e9bda-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="e9bda-104">В этом разделе вы узнаете, как устанавливать Presto в кластерах HDInsight Hadoop с помощью действий скрипта.</span><span class="sxs-lookup"><span data-stu-id="e9bda-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="e9bda-105">Вы также узнаете, как устанавливать Airpal в имеющемся кластере Presto HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9bda-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9bda-106">Для выполнения действий, описанных в этом документе, необходим **кластер Hadoop для HDInsight 3.5** под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="e9bda-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="e9bda-107">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e9bda-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e9bda-108">Дополнительные сведения см. в статье [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="e9bda-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="e9bda-109">Что такое Presto?</span><span class="sxs-lookup"><span data-stu-id="e9bda-109">What is Presto?</span></span>
<span data-ttu-id="e9bda-110">[Presto](https://prestodb.io/overview.html) представляет собой быстрый распределенный модуль SQL-запросов для больших данных.</span><span class="sxs-lookup"><span data-stu-id="e9bda-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="e9bda-111">Presto подходит для интерактивных запросов петабайт данных.</span><span class="sxs-lookup"><span data-stu-id="e9bda-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="e9bda-112">Дополнительные сведения о компонентах Presto и их совместной работе см. в статье [Presto Concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst) (Концепции Presto).</span><span class="sxs-lookup"><span data-stu-id="e9bda-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="e9bda-113">Компоненты, предоставляемые вместе с кластером HDInsight, поддерживаются в полном объеме. Служба поддержки Майкрософт поможет вам выявить и устранить проблемы, связанные с этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="e9bda-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="e9bda-114">Настраиваемые компоненты, такие как Presto, получают ограниченную коммерчески оправданную поддержку, способствующую дальнейшей диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="e9bda-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="e9bda-115">В результате проблема может быть устранена, либо вас могут попросить воспользоваться доступными каналами по технологиям с открытым исходным кодом, чтобы связаться с экспертами в данной области.</span><span class="sxs-lookup"><span data-stu-id="e9bda-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="e9bda-116">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="e9bda-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="e9bda-117">Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="e9bda-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="e9bda-118">Установка Presto с помощью действия скрипта</span><span class="sxs-lookup"><span data-stu-id="e9bda-118">Install Presto using script action</span></span>

<span data-ttu-id="e9bda-119">Этот раздел содержит инструкции по использованию примера сценария при создании нового кластера с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e9bda-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="e9bda-120">Начните подготовку кластера с помощью действий, описанных в статье [Создание кластеров под управлением Linux в HDInsight с помощью портала Azure](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="e9bda-121">Убедитесь, что создаете кластер с помощью процесса создания **пользовательского** кластера.</span><span class="sxs-lookup"><span data-stu-id="e9bda-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="e9bda-122">Необходимо убедиться, что создаваемый кластер соответствует следующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="e9bda-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="e9bda-123">а.</span><span class="sxs-lookup"><span data-stu-id="e9bda-123">a.</span></span> <span data-ttu-id="e9bda-124">Это должен быть кластер Hadoop в HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="e9bda-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="e9bda-125">b.</span><span class="sxs-lookup"><span data-stu-id="e9bda-125">b.</span></span> <span data-ttu-id="e9bda-126">Он должен использовать хранилище Azure в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="e9bda-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="e9bda-127">Использование Presto в кластере с Azure Data Lake Store в качестве хранилища пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e9bda-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Создание кластера HDInsight с использованием настраиваемых параметров](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="e9bda-129">В колонке **Дополнительные параметры** выберите **Действия скрипта** и введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e9bda-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="e9bda-130">**ИМЯ**: введите понятное имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="e9bda-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="e9bda-131">**URI bash-скрипта**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="e9bda-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="e9bda-132">**ГОЛОВНОЙ**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="e9bda-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="e9bda-133">**Рабочая роль**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="e9bda-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="e9bda-134">**ZOOKEEPER**: снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="e9bda-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="e9bda-135">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="e9bda-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="e9bda-136">В нижней части колонки **Действия скрипта** нажмите кнопку **Выбрать**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="e9bda-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="e9bda-137">В нижней части колонки **Дополнительные параметры** нажмите кнопку **Выбрать**, чтобы сохранить данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e9bda-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="e9bda-138">Продолжите подготовку кластера к работе, как описано в статье [Подготовка кластеров HDInsight на основе Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e9bda-139">Для выполнения действий этого сценария также можно использовать Azure PowerShell, Azure CLI, пакет SDK .NET для HDInsight или шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9bda-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="e9bda-140">Действия сценария также можно применять к уже работающим кластерам.</span><span class="sxs-lookup"><span data-stu-id="e9bda-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="e9bda-141">Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="e9bda-142">Использование Presto с HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9bda-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="e9bda-143">Выполните следующие действия, чтобы использовать Presto в кластере HDInsight после установки по процедуре, описанной выше.</span><span class="sxs-lookup"><span data-stu-id="e9bda-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="e9bda-144">Подключитесь к кластеру HDInsight с помощью протокола SSH:</span><span class="sxs-lookup"><span data-stu-id="e9bda-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="e9bda-145">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="e9bda-146">Запустите оболочку Presto, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e9bda-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="e9bda-147">Выполните запрос в примере таблицы **hivesampletable**, которая доступна во всех кластерах HDInsight по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e9bda-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="e9bda-148">По умолчанию соединители [Hive](https://prestodb.io/docs/current/connector/hive.html) и [TPCH](https://prestodb.io/docs/current/connector/tpch.html) для Presto уже настроены.</span><span class="sxs-lookup"><span data-stu-id="e9bda-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="e9bda-149">Соединитель Hive настроен на использование установки Hive по умолчанию, поэтому все таблицы из Hive будут автоматически отображаться в Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="e9bda-150">Подробное описание использования Presto см. в [документации по Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="e9bda-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="e9bda-151">Использование Airpal с Presto</span><span class="sxs-lookup"><span data-stu-id="e9bda-151">Use Airpal with Presto</span></span>

<span data-ttu-id="e9bda-152">[Airpal](https://github.com/airbnb/airpal#airpal) является веб-интерфейсом запросов с открытым кодом для Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="e9bda-153">Дополнительные сведения об Airpal см. в [документации по Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="e9bda-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="e9bda-154">В этом разделе мы рассмотрим порядок действий для **установки Airpal на граничном узле** кластера HDInsight Hadoop, в котором уже установлен Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="e9bda-155">Это гарантирует доступность веб-интерфейса запросов Airpal через Интернет.</span><span class="sxs-lookup"><span data-stu-id="e9bda-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="e9bda-156">Подключитесь по протоколу SSH к головному узлу кластера HDInsight, в котором уже установлен Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="e9bda-157">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e9bda-158">После подключения выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e9bda-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="e9bda-159">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e9bda-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="e9bda-160">В выходных данных запомните значение свойства **value**.</span><span class="sxs-lookup"><span data-stu-id="e9bda-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="e9bda-161">Оно потребуется при установке Airpal на граничном узле кластера.</span><span class="sxs-lookup"><span data-stu-id="e9bda-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="e9bda-162">В приведенном выше примере нужным значением будет **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="e9bda-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="e9bda-163">Используйте **[этот](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** шаблон для создания граничного узла кластера HDInsight и введите значения, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="e9bda-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![Установка HDInsight Airpal в кластер Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="e9bda-165">Щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="e9bda-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="e9bda-166">После применения изменений к конфигурации кластера можно получить доступ к веб-интерфейсу Airpal, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9bda-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="e9bda-167">а.</span><span class="sxs-lookup"><span data-stu-id="e9bda-167">a.</span></span> <span data-ttu-id="e9bda-168">В колонке кластера щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="e9bda-168">From the cluster blade, click **Applications**.</span></span>

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="e9bda-170">b.</span><span class="sxs-lookup"><span data-stu-id="e9bda-170">b.</span></span> <span data-ttu-id="e9bda-171">В колонке**Установленные приложения**, щелкните **Портал** напротив airpal.</span><span class="sxs-lookup"><span data-stu-id="e9bda-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="e9bda-173">c.</span><span class="sxs-lookup"><span data-stu-id="e9bda-173">c.</span></span> <span data-ttu-id="e9bda-174">При появлении запроса введите учетные данные администратора, указанные при создании кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e9bda-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="e9bda-175">Настройка установки Presto в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9bda-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="e9bda-176">После установки Presto в кластер HDInsight можно настроить установку, чтобы внести изменения, такие как обновление параметров памяти, изменение соединителей и т. д. Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9bda-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="e9bda-177">Подключитесь по протоколу SSH к головному узлу кластера HDInsight, в котором уже установлен Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="e9bda-178">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e9bda-179">Внесите изменения конфигурации в файл `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="e9bda-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="e9bda-180">Дополнительные сведения о конфигурации см. в статье [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Конфигурация Presto для кластеров на базе YARN).</span><span class="sxs-lookup"><span data-stu-id="e9bda-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="e9bda-181">Остановите и отмените текущий выполняемый экземпляр Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="e9bda-182">Запустите новый экземпляр Presto с настройками.</span><span class="sxs-lookup"><span data-stu-id="e9bda-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="e9bda-183">Дождитесь готовности нового экземпляра и запишите адрес координатора Presto.</span><span class="sxs-lookup"><span data-stu-id="e9bda-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="e9bda-184">Создание тестовых данных для кластеров HDInsight под управлением Presto</span><span class="sxs-lookup"><span data-stu-id="e9bda-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="e9bda-185">TPC-DS — это отраслевой стандарт для измерения производительности многих систем поддержки принятия решений, включая системы больших данных.</span><span class="sxs-lookup"><span data-stu-id="e9bda-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="e9bda-186">Presto можно использовать в кластерах HDInsight, чтобы создавать данные и сравнивать их с собственными данными тестирования HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9bda-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="e9bda-187">Дополнительные сведения см. [здесь](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="e9bda-188">См. также</span><span class="sxs-lookup"><span data-stu-id="e9bda-188">See also</span></span>
* <span data-ttu-id="e9bda-189">[Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="e9bda-190">Hue — это веб-интерфейс, который позволяет легко создавать, запускать и сохранять задания Pig и Hive, а также просматривать содержимое хранилища по умолчанию для вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9bda-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="e9bda-191">[Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="e9bda-192">Используйте настройки кластера для установки Giraph в кластерах HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e9bda-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="e9bda-193">Giraph позволяет выполнять обработку графов с использованием Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9bda-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="e9bda-194">[Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e9bda-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="e9bda-195">Используйте настройки кластера для установки Solr в кластерах HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e9bda-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="e9bda-196">Solr позволяет вести расширенный поиск по хранимым данным.</span><span class="sxs-lookup"><span data-stu-id="e9bda-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
