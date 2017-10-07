---
title: "кластеры Presto в Azure HDInsight Linux aaaInstall | Документы Microsoft"
description: "Узнайте, как tooinstall Presto и Airpal на основе Linux HDInsight Hadoop кластеры, использующие действий скрипта."
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
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="b70de-103">Установка и использование Presto в кластерах HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b70de-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="b70de-104">В этом разделе вы узнаете, как кластеры tooinstall Presto на HDInsight Hadoop с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="b70de-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="b70de-105">Вы также узнаете, как tooinstall Airpal в существующем кластере Presto HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b70de-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b70de-106">Hello в данном пошаговом руководстве требуется **кластера HDInsight 3.5 Hadoop** , использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="b70de-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="b70de-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b70de-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b70de-108">Дополнительные сведения см. в статье [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="b70de-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="b70de-109">Что такое Presto?</span><span class="sxs-lookup"><span data-stu-id="b70de-109">What is Presto?</span></span>
<span data-ttu-id="b70de-110">[Presto](https://prestodb.io/overview.html) представляет собой быстрый распределенный модуль SQL-запросов для больших данных.</span><span class="sxs-lookup"><span data-stu-id="b70de-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="b70de-111">Presto подходит для интерактивных запросов петабайт данных.</span><span class="sxs-lookup"><span data-stu-id="b70de-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="b70de-112">Дополнительные сведения о компонентах hello Presto и как они работают вместе. в разделе [появится понятия](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="b70de-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="b70de-113">Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.</span><span class="sxs-lookup"><span data-stu-id="b70de-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="b70de-114">Пользовательские компоненты, такие как Presto получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="b70de-115">Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии.</span><span class="sxs-lookup"><span data-stu-id="b70de-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="b70de-116">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="b70de-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="b70de-117">Установка Presto с помощью действия скрипта</span><span class="sxs-lookup"><span data-stu-id="b70de-117">Install Presto using script action</span></span>

<span data-ttu-id="b70de-118">В этом разделе описано, как toouse hello образец скрипта при создании нового кластера с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b70de-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="b70de-119">Запуск подготовки кластера с помощью действия hello в [кластеры HDInsight под управлением Linux подготовки](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="b70de-120">Убедитесь, что вы создаете с помощью hello кластер hello **настраиваемый** кластера создания потока.</span><span class="sxs-lookup"><span data-stu-id="b70de-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="b70de-121">Необходимо убедиться, что при создании кластера hello соответствует hello следующие требования.</span><span class="sxs-lookup"><span data-stu-id="b70de-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="b70de-122">а.</span><span class="sxs-lookup"><span data-stu-id="b70de-122">a.</span></span> <span data-ttu-id="b70de-123">Это должен быть кластер Hadoop в HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="b70de-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="b70de-124">b.</span><span class="sxs-lookup"><span data-stu-id="b70de-124">b.</span></span> <span data-ttu-id="b70de-125">Оно должно использовать хранилище Azure как hello хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="b70de-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="b70de-126">С помощью Presto на кластер, использующий в качестве варианта хранилища hello хранилища Озера данных Azure пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b70de-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Создание кластера HDInsight с использованием настраиваемых параметров](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="b70de-128">На hello **Дополнительные параметры** колонке выберите **действия скрипта**и укажите следующие сведения hello:</span><span class="sxs-lookup"><span data-stu-id="b70de-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="b70de-129">**ИМЯ**: Введите понятное имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="b70de-130">**URI bash-скрипта**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="b70de-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="b70de-131">**ГОЛОВНОЙ**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="b70de-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="b70de-132">**Рабочая роль**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="b70de-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="b70de-133">**ZOOKEEPER**: снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="b70de-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="b70de-134">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="b70de-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="b70de-135">Внизу hello hello **действия скрипта** колонке щелкните hello **выберите** конфигурация hello toosave кнопок.</span><span class="sxs-lookup"><span data-stu-id="b70de-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="b70de-136">Щелкните hello **выберите** кнопку внизу hello hello **Дополнительные параметры** сведения о конфигурации hello toosave колонку.</span><span class="sxs-lookup"><span data-stu-id="b70de-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="b70de-137">Продолжить подготовки кластера hello, как описано в [кластеры HDInsight под управлением Linux подготовки](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b70de-138">Действия сценариев используется tooapply также может быть Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK или шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b70de-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="b70de-139">Можно также применить tooalready действия сценария работающие кластеры.</span><span class="sxs-lookup"><span data-stu-id="b70de-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="b70de-140">Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="b70de-141">Использование Presto с HDInsight</span><span class="sxs-lookup"><span data-stu-id="b70de-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="b70de-142">Выполните следующие шаги toouse Presto в кластер HDInsight после установки с помощью hello действия, описанные выше hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="b70de-143">Подключите кластер HDInsight toohello с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="b70de-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="b70de-144">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="b70de-145">Запустите консоль появится hello, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="b70de-146">Выполните запрос в примере таблицы **hivesampletable**, которая доступна во всех кластерах HDInsight по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b70de-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="b70de-147">По умолчанию соединители [Hive](https://prestodb.io/docs/current/connector/hive.html) и [TPCH](https://prestodb.io/docs/current/connector/tpch.html) для Presto уже настроены.</span><span class="sxs-lookup"><span data-stu-id="b70de-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="b70de-148">Соединитель куст — настроенное toouse hello установки по умолчанию установлен Hive, таким образом, все таблицы hello из куста автоматически отображается на Presto.</span><span class="sxs-lookup"><span data-stu-id="b70de-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="b70de-149">Подробное описание использования Presto см. в [документации по Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="b70de-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="b70de-150">Использование Airpal с Presto</span><span class="sxs-lookup"><span data-stu-id="b70de-150">Use Airpal with Presto</span></span>

<span data-ttu-id="b70de-151">[Airpal](https://github.com/airbnb/airpal#airpal) является веб-интерфейсом запросов с открытым кодом для Presto.</span><span class="sxs-lookup"><span data-stu-id="b70de-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="b70de-152">Дополнительные сведения об Airpal см. в [документации по Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="b70de-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="b70de-153">В этом разделе мы рассмотрим действия hello слишком**установить Airpal на hello edgenode** кластер HDInsight Hadoop, уже содержит Presto установлена.</span><span class="sxs-lookup"><span data-stu-id="b70de-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="b70de-154">Это гарантирует, что запрос, hello Airpal веб-интерфейс доступна через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="b70de-155">С помощью SSH, подключиться к головному узлу кластера HDInsight hello, если оно Presto toohello:</span><span class="sxs-lookup"><span data-stu-id="b70de-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="b70de-156">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b70de-157">После подключения, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="b70de-158">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b70de-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="b70de-159">Hello в выходных данных, отметьте значение hello hello **значение** свойства.</span><span class="sxs-lookup"><span data-stu-id="b70de-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="b70de-160">Он потребуется при установке Airpal на edgenode hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b70de-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="b70de-161">Из выходных данных hello выше значение hello, вам потребуется — **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="b70de-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="b70de-162">Использовать шаблон hello  **[здесь](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate HDInsight кластера edgenode и предоставления значения hello, как показано в следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="b70de-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![Установка HDInsight Airpal в кластер Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="b70de-164">Щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="b70de-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="b70de-165">После изменений hello примененных toohello конфигурации кластера, доступны hello Airpal веб-интерфейса с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="b70de-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="b70de-166">а.</span><span class="sxs-lookup"><span data-stu-id="b70de-166">a.</span></span> <span data-ttu-id="b70de-167">Из колонки hello кластера, нажмите кнопку **приложений**.</span><span class="sxs-lookup"><span data-stu-id="b70de-167">From hello cluster blade, click **Applications**.</span></span>

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="b70de-169">b.</span><span class="sxs-lookup"><span data-stu-id="b70de-169">b.</span></span> <span data-ttu-id="b70de-170">Из hello **установленные приложения** колонка, щелкните **портала** от airpal.</span><span class="sxs-lookup"><span data-stu-id="b70de-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="b70de-172">c.</span><span class="sxs-lookup"><span data-stu-id="b70de-172">c.</span></span> <span data-ttu-id="b70de-173">При появлении запроса введите учетные данные администратора hello, указанный при создании hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b70de-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="b70de-174">Настройка установки Presto в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="b70de-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="b70de-175">После установки Presto в кластере HDInsight Hadoop, можно настроить hello установки toomake изменения, такие как параметры памяти обновления, измените соединителей, и т. д. Выполните hello, поэтому следующие шаги toodo.</span><span class="sxs-lookup"><span data-stu-id="b70de-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="b70de-176">С помощью SSH, подключиться к головному узлу кластера HDInsight hello, если оно Presto toohello:</span><span class="sxs-lookup"><span data-stu-id="b70de-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="b70de-177">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b70de-178">Внесите изменения в конфигурацию в файле hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="b70de-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="b70de-179">Дополнительные сведения о конфигурации см. в статье [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Конфигурация Presto для кластеров на базе YARN).</span><span class="sxs-lookup"><span data-stu-id="b70de-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="b70de-180">Остановите и завершения текущего выполняемого экземпляра hello Presto.</span><span class="sxs-lookup"><span data-stu-id="b70de-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="b70de-181">Запустите новый экземпляр Presto с настройкой hello.</span><span class="sxs-lookup"><span data-stu-id="b70de-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="b70de-182">Дождитесь hello новый экземпляр toobe готовности и запишите адрес появится координатора.</span><span class="sxs-lookup"><span data-stu-id="b70de-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="b70de-183">Создание тестовых данных для кластеров HDInsight под управлением Presto</span><span class="sxs-lookup"><span data-stu-id="b70de-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="b70de-184">TPC-доменных служб Active Directory — hello стандартный для измерения производительности hello многих систем поддержки принятия решений, включая систем большие наборы данных.</span><span class="sxs-lookup"><span data-stu-id="b70de-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="b70de-185">Можно использовать Presto данных toogenerate кластеров HDInsight и оценить, сравнивает его с данными тестирования HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b70de-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="b70de-186">Дополнительные сведения см. [здесь](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="b70de-187">См. также</span><span class="sxs-lookup"><span data-stu-id="b70de-187">See also</span></span>
* <span data-ttu-id="b70de-188">[Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="b70de-189">Цветовым тоном является веб-интерфейса, который позволяет легко toocreate, запустите и сохраните задания Pig и Hive, также как и в случае найдите hello хранилища по умолчанию для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b70de-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="b70de-190">[Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="b70de-191">Используйте tooinstall настройки кластера кластеров Giraph на HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b70de-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="b70de-192">Giraph дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b70de-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="b70de-193">[Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b70de-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="b70de-194">Используйте tooinstall настройки кластера кластеров Solr на HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b70de-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="b70de-195">Solr позволяет выполнять операции поиска мощные tooperform хранимых данных.</span><span class="sxs-lookup"><span data-stu-id="b70de-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
