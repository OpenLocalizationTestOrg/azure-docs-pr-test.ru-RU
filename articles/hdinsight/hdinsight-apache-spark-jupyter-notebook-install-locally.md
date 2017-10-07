---
title: "aaaInstall Jupyter локально & подключения кластера Azure HDInsight Spark tooan | Документы Microsoft"
description: "Узнайте, как книжке Jupyter tooinstall на локальном компьютере и его подключения кластера tooan Apache Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="be92f-103">Установка книжке Jupyter на вашем компьютере и подключение tooApache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="be92f-104">В этой статье вы узнаете, как записной книжки Jupyter tooinstall с hello пользовательских PySpark (для Python) и ядра Spark (для Scala) с усилить magic и подключения кластера HDInsight tooan записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="be92f-105">Может быть несколько причин tooinstall Jupyter на локальном компьютере и может быть также некоторые проблемы.</span><span class="sxs-lookup"><span data-stu-id="be92f-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="be92f-106">Для получения дополнительных сведений в данном разделе hello [Зачем устанавливать Jupyter на моем компьютере](#why-should-i-install-jupyter-on-my-computer) конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be92f-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="be92f-107">Существует три ключевых действия, участвующие в процессе установки Jupyter и hello Spark magic на компьютере.</span><span class="sxs-lookup"><span data-stu-id="be92f-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="be92f-108">Установка записной книжки Jupyter</span><span class="sxs-lookup"><span data-stu-id="be92f-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="be92f-109">Установите hello PySpark и Spark ядер hello Spark magic</span><span class="sxs-lookup"><span data-stu-id="be92f-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="be92f-110">Настройка Spark magic tooaccess кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="be92f-111">Дополнительные сведения о пользовательских ядер hello и magic Spark hello для записные книжки Jupyter с кластером HDInsight см. в разделе [кластеры ядер, доступных для записные книжки Jupyter с Apache Spark Linux в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="be92f-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be92f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be92f-112">Prerequisites</span></span>
<span data-ttu-id="be92f-113">Hello предварительные требования, перечисленные здесь не для установки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="be92f-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="be92f-114">Это подключение hello кластера HDInsight tooan Jupyter записной книжки после установки записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="be92f-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="be92f-115">An Azure subscription.</span></span> <span data-ttu-id="be92f-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="be92f-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="be92f-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be92f-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="be92f-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="be92f-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="be92f-119">Установка записной книжки Jupyter на компьютер</span><span class="sxs-lookup"><span data-stu-id="be92f-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="be92f-120">Перед установкой записных книжек Jupyter необходимо установить Python.</span><span class="sxs-lookup"><span data-stu-id="be92f-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="be92f-121">Python и Jupyter доступны как часть hello [дистрибутив Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="be92f-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="be92f-122">При установке Anaconda устанавливается дистрибутив Python.</span><span class="sxs-lookup"><span data-stu-id="be92f-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="be92f-123">После установки Anaconda, чтобы добавить hello Jupyter установки, запустите соответствующие команды.</span><span class="sxs-lookup"><span data-stu-id="be92f-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="be92f-124">Загрузите hello [Anaconda установщика](https://www.continuum.io/downloads) для платформы и hello выполнения установки.</span><span class="sxs-lookup"><span data-stu-id="be92f-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="be92f-125">Во время выполнения мастера установки hello убедитесь, что выбран hello параметр tooadd Anaconda tooyour переменной PATH.</span><span class="sxs-lookup"><span data-stu-id="be92f-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="be92f-126">Выполните следующие команды tooinstall Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="be92f-127">Дополнительные сведения об установке Jupyter см. [здесь](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="be92f-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="be92f-128">Установка ядра hello и Spark magic</span><span class="sxs-lookup"><span data-stu-id="be92f-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="be92f-129">Инструкции по как tooinstall hello Spark magic, hello PySpark и Spark ядер, следуйте инструкциям по установке hello в hello [sparkmagic документации](https://github.com/jupyter-incubator/sparkmagic#installation) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="be92f-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="be92f-130">Hello первым шагом в документации magic Spark hello предлагает магическое tooinstall Spark.</span><span class="sxs-lookup"><span data-stu-id="be92f-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="be92f-131">Замените первый шаг в ссылке hello hello, следующие команды, в зависимости от версии hello hello кластера HDInsight, которую вы будете подключаться.</span><span class="sxs-lookup"><span data-stu-id="be92f-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="be92f-132">Затем выполните оставшиеся действия, описанные в документации magic Spark hello hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="be92f-133">Если вы хотите tooinstall hello других ядер, необходимо выполнить шаг 3 в hello Spark magic инструкции см.</span><span class="sxs-lookup"><span data-stu-id="be92f-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="be92f-134">Для кластеров версии 3.4 установите sparkmagic версии 0.2.3, выполнив команду `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="be92f-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="be92f-135">Для кластеров версий 3.5 и 3.6 установите sparkmagic версии 0.11.2, выполнив команду `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="be92f-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="be92f-136">Настройка кластера Spark tooHDInsight magic tooconnect Spark</span><span class="sxs-lookup"><span data-stu-id="be92f-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="be92f-137">В этом разделе Настройка magic Spark hello, установленного ранее tooconnect tooan Apache Spark кластер, необходимо уже созданных в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be92f-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="be92f-138">Hello Jupyter сведения о конфигурации обычно хранятся в домашнем каталоге hello пользователей.</span><span class="sxs-lookup"><span data-stu-id="be92f-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="be92f-139">toolocate вашим домашним каталогом на любой платформе операционной системы, тип hello следующие команды.</span><span class="sxs-lookup"><span data-stu-id="be92f-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="be92f-140">Запустите консоль hello Python.</span><span class="sxs-lookup"><span data-stu-id="be92f-140">Start hello Python shell.</span></span> <span data-ttu-id="be92f-141">В окно командной строки введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="be92f-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="be92f-142">Hello оболочки Python введите hello, следующая команда toofind hello домашнего каталога.</span><span class="sxs-lookup"><span data-stu-id="be92f-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="be92f-143">Перейдите в корневой каталог toohello и создайте папку с именем **.sparkmagic** , если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="be92f-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="be92f-144">В папке hello, создайте файл с именем **config.json** и добавьте следующий фрагмент JSON внутри него hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="be92f-145">Замените **{USERNAME}**, **{CLUSTERDNSNAME}** и **{BASE64ENCODEDPASSWORD}** соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="be92f-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="be92f-146">Фактический пароль можно использовать несколько служебных программ избранные языка программирования и зашифрованный пароль online toogenerate кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="be92f-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="be92f-147">Настройка параметров правой периодического сигнала hello в `config.json`.</span><span class="sxs-lookup"><span data-stu-id="be92f-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="be92f-148">Эти параметры следует добавить во же уровня как hello hello `kernel_python_credentials` и `kernel_scala_credentials` фрагменты вашей добавленные ранее.</span><span class="sxs-lookup"><span data-stu-id="be92f-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="be92f-149">Пример hello как и где tooadd параметры периодических сигналов, см. в этой [config.json пример](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="be92f-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="be92f-150">Для `sparkmagic 0.2.3` (кластеры версии 3.4) добавьте:</span><span class="sxs-lookup"><span data-stu-id="be92f-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="be92f-151">Для `sparkmagic 0.11.2` (кластеры версий 3.5 и 3.6) добавьте:</span><span class="sxs-lookup"><span data-stu-id="be92f-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="be92f-152">Тактовые импульсы отправляются tooensure сеансы не попадают.</span><span class="sxs-lookup"><span data-stu-id="be92f-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="be92f-153">При переходит toosleep или завершить работу компьютера, не передается пульса hello, приведет к hello сеанса, удаляются.</span><span class="sxs-lookup"><span data-stu-id="be92f-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="be92f-154">Для v3.4 кластеров, при желании toodisable такое поведение, можно задать hello Livy config `livy.server.interactive.heartbeat.timeout` слишком`0` из hello Ambari пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="be92f-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="be92f-155">Для кластеров версии 3.5 если конфигурации hello 3.5 выше, не устанавливайте hello сеанса не удаляются.</span><span class="sxs-lookup"><span data-stu-id="be92f-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="be92f-156">Запустите Jupyter.</span><span class="sxs-lookup"><span data-stu-id="be92f-156">Start Jupyter.</span></span> <span data-ttu-id="be92f-157">Используйте следующую команду из командной строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="be92f-158">Убедитесь, что можно подключиться toohello кластер, использующий книжке Jupyter hello и могут использовать доступные magic Spark hello с ядром hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="be92f-159">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-159">Perform hello following steps.</span></span>

    <span data-ttu-id="be92f-160">а.</span><span class="sxs-lookup"><span data-stu-id="be92f-160">a.</span></span> <span data-ttu-id="be92f-161">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="be92f-161">Create a new notebook.</span></span> <span data-ttu-id="be92f-162">В правом углу hello, выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="be92f-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="be92f-163">Вы увидите ядра по умолчанию hello **Python2** и hello два новых ядер, которые можно установить **PySpark** и **Spark**.</span><span class="sxs-lookup"><span data-stu-id="be92f-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="be92f-164">Щелкните **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="be92f-164">Click **PySpark**.</span></span>

    <span data-ttu-id="be92f-165">![Ядра в записной книжке Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Ядра в записной книжке Jupyter")</span><span class="sxs-lookup"><span data-stu-id="be92f-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="be92f-166">b.</span><span class="sxs-lookup"><span data-stu-id="be92f-166">b.</span></span> <span data-ttu-id="be92f-167">Запустите следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="be92f-168">Если можно успешно получить выходные данные hello, проверяется кластеру HDInsight toohello соединения.</span><span class="sxs-lookup"><span data-stu-id="be92f-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="be92f-169">Tooupdate hello записной книжки конфигурации tooconnect tooa другой кластер, обновите hello config.json hello новый набор значений, как показано в шаге 3 выше.</span><span class="sxs-lookup"><span data-stu-id="be92f-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="be92f-170">Зачем устанавливать Jupyter на моем компьютере?</span><span class="sxs-lookup"><span data-stu-id="be92f-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="be92f-171">Может быть несколько причин, почему вы хотите tooinstall Jupyter на вашем компьютере и подключить его кластера tooa Spark на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be92f-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="be92f-172">Даже если записные книжки Jupyter уже доступны hello кластере Spark в Azure HDInsight, установка Jupyter на компьютере обеспечивает hello toocreate параметр записных книжек локально, протестировать приложение на запущенному кластеру и затем передать hello портативные компьютеры toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="be92f-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="be92f-173">tooupload hello записных книжек toohello кластера, вы можете отправить их с помощью hello книжке Jupyter, на котором выполняется или hello кластера и сохранить toohello /HdiNotebooks папки в учетной записи хранилища hello, связанной с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="be92f-174">Дополнительные сведения о хранении портативные компьютеры в кластере hello см. в разделе [записные книжки Jupyter хранения](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="be92f-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="be92f-175">Портативные компьютеры hello доступны локально, позволяет подключаться toodifferent Spark кластеров на основе требований вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="be92f-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="be92f-176">Можно использовать GitHub tooimplement системы управления версиями и управления версиями для ноутбуков hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="be92f-177">Вы также можете среде совместной работы, где могут работать несколько пользователей с hello же записной книжке.</span><span class="sxs-lookup"><span data-stu-id="be92f-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="be92f-178">Вы можете работать с записными книжками локально даже без кластера.</span><span class="sxs-lookup"><span data-stu-id="be92f-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="be92f-179">Требуется только tootest кластера записных книжек от, не toomanually управлять записных книжек, либо в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="be92f-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="be92f-180">Он может быть проще tooconfigure собственные локальной среде разработки, чем tooconfigure hello Jupyter установки на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="be92f-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="be92f-181">Вы сможете использовать все hello программного обеспечения, установленных локально без настройки одного или нескольких удаленных кластеров.</span><span class="sxs-lookup"><span data-stu-id="be92f-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="be92f-182">С Jupyter установлен на локальном компьютере, несколько пользователей могут запустить hello же записной книжке hello же Spark кластера на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="be92f-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="be92f-183">В такой ситуации создаются несколько сеансов Livy.</span><span class="sxs-lookup"><span data-stu-id="be92f-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="be92f-184">Если возникли проблемы и требуется, он будет tootrack сложной задачей, принадлежит какой Livy сеанс пользователя toowhich toodebug.</span><span class="sxs-lookup"><span data-stu-id="be92f-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="be92f-185"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="be92f-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="be92f-186">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="be92f-187">Сценарии</span><span class="sxs-lookup"><span data-stu-id="be92f-187">Scenarios</span></span>
* [<span data-ttu-id="be92f-188">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="be92f-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="be92f-189">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="be92f-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="be92f-190">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="be92f-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="be92f-191">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="be92f-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="be92f-192">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="be92f-193">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="be92f-193">Create and run applications</span></span>
* [<span data-ttu-id="be92f-194">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="be92f-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="be92f-195">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="be92f-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="be92f-196">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="be92f-196">Tools and extensions</span></span>
* [<span data-ttu-id="be92f-197">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="be92f-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="be92f-198">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="be92f-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="be92f-199">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="be92f-200">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="be92f-201">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="be92f-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="be92f-202">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="be92f-202">Manage resources</span></span>
* [<span data-ttu-id="be92f-203">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="be92f-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="be92f-204">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="be92f-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
