---
title: "Установка записной книжки Jupyter в локальной среде и ее подключение к кластеру Azure HDInsight Spark | Документы Майкрософт"
description: "Сведения о том, как установить записную книжку Jupyter на компьютере локально и как подключить ее к кластеру Apache Spark в Azure HDInsight."
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="d57ed-103">Установка записной книжки Jupyter на компьютере и ее подключение к Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="d57ed-104">Из этой статьи вы узнаете, как установить записную книжку Jupyter с пользовательскими ядрами PySpark (для Python) и Spark (для Scala) с помощью волшебной команды Spark, а затем подключить эту записную книжку к кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d57ed-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="d57ed-105">Существуют разные причины для установки Jupyter на локальном компьютере, но есть и некоторые трудности.</span><span class="sxs-lookup"><span data-stu-id="d57ed-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="d57ed-106">Дополнительные сведения см. в разделе [Зачем устанавливать Jupyter на компьютер?](#why-should-i-install-jupyter-on-my-computer) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="d57ed-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="d57ed-107">Для установки Jupyter и волшебной команды Spark на ваш компьютер необходимо выполнить три основных действия.</span><span class="sxs-lookup"><span data-stu-id="d57ed-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="d57ed-108">Установка записной книжки Jupyter</span><span class="sxs-lookup"><span data-stu-id="d57ed-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="d57ed-109">Установите ядра PySpark и Spark с помощью волшебной команды Spark</span><span class="sxs-lookup"><span data-stu-id="d57ed-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="d57ed-110">Настройте волшебную команду Spark для доступа к кластеру Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="d57ed-111">Дополнительные сведения о пользовательских ядрах и волшебных командах Spark, доступных для записных книжек Jupyter в кластере HDInsight, см. в статье [Ядра, доступные для использования записными книжками Jupyter с кластерами Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="d57ed-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d57ed-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d57ed-112">Prerequisites</span></span>
<span data-ttu-id="d57ed-113">Указанные здесь предварительные требования относятся не к установке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d57ed-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="d57ed-114">Они относятся к подключению записной книжки Jupyter к кластеру HDInsight после установки записной книжки.</span><span class="sxs-lookup"><span data-stu-id="d57ed-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="d57ed-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d57ed-115">An Azure subscription.</span></span> <span data-ttu-id="d57ed-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d57ed-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d57ed-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d57ed-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="d57ed-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d57ed-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="d57ed-119">Установка записной книжки Jupyter на компьютер</span><span class="sxs-lookup"><span data-stu-id="d57ed-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="d57ed-120">Перед установкой записных книжек Jupyter необходимо установить Python.</span><span class="sxs-lookup"><span data-stu-id="d57ed-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="d57ed-121">Python и Jupyter доступны в составе [дистрибутива Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="d57ed-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="d57ed-122">При установке Anaconda устанавливается дистрибутив Python.</span><span class="sxs-lookup"><span data-stu-id="d57ed-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="d57ed-123">После установки Anaconda выполните соответствующие команды для установки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d57ed-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="d57ed-124">Скачайте [установщик Anaconda](https://www.continuum.io/downloads) для своей платформы и запустите программу установки.</span><span class="sxs-lookup"><span data-stu-id="d57ed-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="d57ed-125">В мастере установки укажите параметр для добавления Anaconda в переменную PATH.</span><span class="sxs-lookup"><span data-stu-id="d57ed-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="d57ed-126">Выполните следующую команду для установки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d57ed-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="d57ed-127">Дополнительные сведения об установке Jupyter см. [здесь](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="d57ed-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="d57ed-128">Установка ядер и волшебной команды Spark</span><span class="sxs-lookup"><span data-stu-id="d57ed-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="d57ed-129">Инструкции по установке волшебной команды Spark, а также ядер PySpark и Spark, см. в [документации по sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="d57ed-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="d57ed-130">Чтобы начать использовать волшебную команду Spark, ее сначала нужно установить. Это — первый шаг, описанный в документации.</span><span class="sxs-lookup"><span data-stu-id="d57ed-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="d57ed-131">Замените этот шаг в ссылке выше приведенными ниже командами с учетом версии кластера HDInsight, к которому вы подключитесь.</span><span class="sxs-lookup"><span data-stu-id="d57ed-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="d57ed-132">После этого выполните остальные шаги в соответствии с документацией по волшебной команде Spark.</span><span class="sxs-lookup"><span data-stu-id="d57ed-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="d57ed-133">Для установки разных ядер необходимо выполнить шаг 3 из раздела инструкций по установке волшебной команды Spark.</span><span class="sxs-lookup"><span data-stu-id="d57ed-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="d57ed-134">Для кластеров версии 3.4 установите sparkmagic версии 0.2.3, выполнив команду `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="d57ed-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="d57ed-135">Для кластеров версий 3.5 и 3.6 установите sparkmagic версии 0.11.2, выполнив команду `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="d57ed-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="d57ed-136">Настройка волшебной команды Spark для подключения к кластеру HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d57ed-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="d57ed-137">В этом разделе вы настроите подключение волшебной команды Spark, установленную ранее, к кластеру Apache Spark, который вы уже создали в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d57ed-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="d57ed-138">Сведения о конфигурации Jupyter обычно хранятся в домашнем каталоге пользователей.</span><span class="sxs-lookup"><span data-stu-id="d57ed-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="d57ed-139">Чтобы найти домашний каталог, введите следующие команды (они подходят для любой платформы ОС).</span><span class="sxs-lookup"><span data-stu-id="d57ed-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="d57ed-140">Запустите оболочку Python.</span><span class="sxs-lookup"><span data-stu-id="d57ed-140">Start the Python shell.</span></span> <span data-ttu-id="d57ed-141">В командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d57ed-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="d57ed-142">В оболочке Python введите следующую команду, чтобы найти домашний каталог.</span><span class="sxs-lookup"><span data-stu-id="d57ed-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="d57ed-143">Перейдите в домашний каталог и создайте папку с именем **.sparkmagic** , если ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="d57ed-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="d57ed-144">В этой папке создайте файл **config.json** и добавьте в него следующий фрагмент кода JSON.</span><span class="sxs-lookup"><span data-stu-id="d57ed-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="d57ed-145">Замените **{USERNAME}**, **{CLUSTERDNSNAME}** и **{BASE64ENCODEDPASSWORD}** соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="d57ed-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="d57ed-146">Для создания пароля в кодировке base64 вы можете использовать разные служебные программы на предпочитаемом языке программирования или средства, доступные в Интернете.</span><span class="sxs-lookup"><span data-stu-id="d57ed-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="d57ed-147">Правильно настройте параметры пульса в `config.json`.</span><span class="sxs-lookup"><span data-stu-id="d57ed-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="d57ed-148">Эти параметры необходимо добавить на одном уровне с фрагментами `kernel_python_credentials` и `kernel_scala_credentials`, которые были добавлены ранее.</span><span class="sxs-lookup"><span data-stu-id="d57ed-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="d57ed-149">В этом [примере файла config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json) показано, как и где добавляются параметры пульса.</span><span class="sxs-lookup"><span data-stu-id="d57ed-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="d57ed-150">Для `sparkmagic 0.2.3` (кластеры версии 3.4) добавьте:</span><span class="sxs-lookup"><span data-stu-id="d57ed-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="d57ed-151">Для `sparkmagic 0.11.2` (кластеры версий 3.5 и 3.6) добавьте:</span><span class="sxs-lookup"><span data-stu-id="d57ed-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="d57ed-152">Сигналы пульса отправляются, чтобы предотвратить утечку сеансов.</span><span class="sxs-lookup"><span data-stu-id="d57ed-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="d57ed-153">При переходе в спящий режим или завершении работы компьютера пульс не отправляется, что приводит к очистке сеанса.</span><span class="sxs-lookup"><span data-stu-id="d57ed-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="d57ed-154">Если вы хотите отключить такое поведение для кластеров версии 3.4, то можете настроить для параметра Livy `livy.server.interactive.heartbeat.timeout` значение `0` с помощью пользовательского интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="d57ed-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="d57ed-155">Если для кластеров версии 3.5 не настроить соответствующую конфигурацию, приведенную выше, то сеанс не будет удален.</span><span class="sxs-lookup"><span data-stu-id="d57ed-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="d57ed-156">Запустите Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d57ed-156">Start Jupyter.</span></span> <span data-ttu-id="d57ed-157">Выполните следующую команду из командной строки.</span><span class="sxs-lookup"><span data-stu-id="d57ed-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="d57ed-158">Убедитесь, что вы можете подключиться к кластеру с помощью записной книжки Jupyter и использовать волшебную команду Spark с ядрами.</span><span class="sxs-lookup"><span data-stu-id="d57ed-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="d57ed-159">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d57ed-159">Perform the following steps.</span></span>

    <span data-ttu-id="d57ed-160">а.</span><span class="sxs-lookup"><span data-stu-id="d57ed-160">a.</span></span> <span data-ttu-id="d57ed-161">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="d57ed-161">Create a new notebook.</span></span> <span data-ttu-id="d57ed-162">В правом верхнем углу щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d57ed-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="d57ed-163">Вы должны увидеть ядро по умолчанию **Python2** и два новых ядра, которые вы установили: **PySpark** и **Spark**.</span><span class="sxs-lookup"><span data-stu-id="d57ed-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="d57ed-164">Щелкните **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="d57ed-164">Click **PySpark**.</span></span>

    <span data-ttu-id="d57ed-165">![Ядра в записной книжке Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Ядра в записной книжке Jupyter")</span><span class="sxs-lookup"><span data-stu-id="d57ed-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="d57ed-166">b.</span><span class="sxs-lookup"><span data-stu-id="d57ed-166">b.</span></span> <span data-ttu-id="d57ed-167">Запустите следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="d57ed-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="d57ed-168">Если вы успешно получили выходные данные, подключение к кластеру HDInsight работает.</span><span class="sxs-lookup"><span data-stu-id="d57ed-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="d57ed-169">Если вы хотите обновить конфигурацию записной книжки для подключения к другому кластеру, измените файл config.json, указав новый набор значений, как показано на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="d57ed-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="d57ed-170">Зачем устанавливать Jupyter на моем компьютере?</span><span class="sxs-lookup"><span data-stu-id="d57ed-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="d57ed-171">Может быть несколько причин, по которым вам потребуется установить на компьютер Jupyter и подключить его к кластеру Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d57ed-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="d57ed-172">Хотя записные книжки Jupyter уже доступны в кластере Spark в Azure HDInsight, после их установки на компьютер вы сможете создавать записные книжки локально, тестировать приложения на работающем кластере и отправлять записные книжки в кластер.</span><span class="sxs-lookup"><span data-stu-id="d57ed-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="d57ed-173">Для отправки записных книжек в кластер можно отправить их с помощью записной книжки Jupyter, которая запущена на кластере, или сохранить их в папке /HdiNotebooks в учетной записи хранения, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="d57ed-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="d57ed-174">Дополнительные сведения о хранении записных книжек в кластере см. в разделе [Где хранятся записные книжки](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored).</span><span class="sxs-lookup"><span data-stu-id="d57ed-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="d57ed-175">С помощью локально доступных записных книжек вы сможете подключиться к различным кластерам Spark в зависимости от потребностей вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d57ed-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="d57ed-176">Можно использовать GitHub для реализации системы управления версиями, чтобы контролировать версии записных книжек.</span><span class="sxs-lookup"><span data-stu-id="d57ed-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="d57ed-177">Вы также можете создать среду совместной работы, в которой несколько пользователей будут работать с одной записной книжкой.</span><span class="sxs-lookup"><span data-stu-id="d57ed-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="d57ed-178">Вы можете работать с записными книжками локально даже без кластера.</span><span class="sxs-lookup"><span data-stu-id="d57ed-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="d57ed-179">Кластер нужен только для тестирования записных книжек, но не обязателен для ручного управления записными книжками или средой разработки.</span><span class="sxs-lookup"><span data-stu-id="d57ed-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="d57ed-180">Возможно, вам будет проще настроить локальную среду разработки, чем настраивать установку Jupyter в кластере.</span><span class="sxs-lookup"><span data-stu-id="d57ed-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="d57ed-181">Вы можете спокойно пользоваться любым программным обеспечением, установленным локально, не настраивая удаленные кластеры.</span><span class="sxs-lookup"><span data-stu-id="d57ed-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="d57ed-182">Если Jupyter установлен на локальном компьютере, несколько пользователей могут одновременно запустить одну и ту же записную книжку в одном кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="d57ed-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="d57ed-183">В такой ситуации создаются несколько сеансов Livy.</span><span class="sxs-lookup"><span data-stu-id="d57ed-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="d57ed-184">Если вы столкнетесь с проблемами и начнете их отладку, вам будет сложно определить, какой сеанс Livy какому пользователю принадлежит.</span><span class="sxs-lookup"><span data-stu-id="d57ed-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="d57ed-185"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d57ed-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d57ed-186">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d57ed-187">Сценарии</span><span class="sxs-lookup"><span data-stu-id="d57ed-187">Scenarios</span></span>
* [<span data-ttu-id="d57ed-188">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="d57ed-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d57ed-189">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="d57ed-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d57ed-190">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="d57ed-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d57ed-191">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="d57ed-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d57ed-192">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d57ed-193">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="d57ed-193">Create and run applications</span></span>
* [<span data-ttu-id="d57ed-194">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="d57ed-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d57ed-195">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="d57ed-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d57ed-196">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="d57ed-196">Tools and extensions</span></span>
* [<span data-ttu-id="d57ed-197">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="d57ed-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d57ed-198">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="d57ed-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d57ed-199">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d57ed-200">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d57ed-201">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="d57ed-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="d57ed-202">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="d57ed-202">Manage resources</span></span>
* [<span data-ttu-id="d57ed-203">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d57ed-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d57ed-204">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="d57ed-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
