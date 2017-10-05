---
title: "Установка RStudio с R Server в кластере HDInsight — Azure | Документы Майкрософт"
description: "Сведения об установке RStudio с R Server в кластере HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="e496f-103">Установка RStudio с R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e496f-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="e496f-104">В этой статье описывается, как установить бесплатную версию [RStudio Server](https://www.rstudio.com/products/rstudio-server/) для сообщества на граничном узле кластера с помощью пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="e496f-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="e496f-105">RStudio Server предоставляет интегрированную среду разработки (IDE) на основе браузера, предназначенную для удаленных клиентов и широко используемую в Linux.</span><span class="sxs-lookup"><span data-stu-id="e496f-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="e496f-106">Для языка R в настоящее время доступно множество интегрированных сред разработки, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="e496f-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="e496f-107">[Инструменты R для Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) от корпорации Майкрософт</span><span class="sxs-lookup"><span data-stu-id="e496f-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="e496f-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="e496f-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="e496f-109">[StatET](http://www.walware.de/goto/statet) на основе Eclipse от компании Walware</span><span class="sxs-lookup"><span data-stu-id="e496f-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="e496f-110">Преимуществом установки RStudio Server на граничном узле кластера HDInsight является получение доступа ко всем функциональным возможностям IDE для разработки и выполнения скриптов R с использованием R Server в кластере.</span><span class="sxs-lookup"><span data-stu-id="e496f-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="e496f-111">Такая конфигурация может обеспечивать значительно более высокую производительность по сравнению с консолью R.</span><span class="sxs-lookup"><span data-stu-id="e496f-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="e496f-112">Процедура, описанная в этой статье, подходит только в том случае, если вы не выбрали установку выпуска RStudio Server для сообщества при подготовке кластера.</span><span class="sxs-lookup"><span data-stu-id="e496f-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="e496f-113">Если вы добавили его во время подготовки, то для доступа к нему можете щелкнуть плитку **Панели мониторинга R Server** в записи портала Azure для своего кластера, а затем щелкнуть плитку **R Studio Server**.</span><span class="sxs-lookup"><span data-stu-id="e496f-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="e496f-114">Если вы хотите использовать коммерческую версию RStudio Server Pro, необходимо выполнить инструкции по установке из [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="e496f-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="e496f-115">Если вы используете кластер, для которого среда R была установлена с помощью [действия по установке скрипта R](hdinsight-hadoop-r-scripts-linux.md), приведенные в этом документе инструкции не будут работать правильно, так как для них требуется сервер R Server в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="e496f-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e496f-116">Prerequisites</span></span>

* <span data-ttu-id="e496f-117">Кластер Azure HDInsight, на котором установлен R Server.</span><span class="sxs-lookup"><span data-stu-id="e496f-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="e496f-118">Инструкции см. в статье [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e496f-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="e496f-119">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="e496f-119">An SSH client.</span></span> <span data-ttu-id="e496f-120">В дистрибутивах Linux и Unix и Macintosh OS X команда `ssh` входит в состав операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e496f-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="e496f-121">Для Windows мы рекомендуем [Cygwin](http://www.redhat.com/services/custom/cygwin/) (с [параметром OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU)) или [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="e496f-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="e496f-122">Установка RStudio в кластере с помощью пользовательского скрипта</span><span class="sxs-lookup"><span data-stu-id="e496f-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="e496f-123">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e496f-123">Here are the steps:</span></span>

1. <span data-ttu-id="e496f-124">Определите граничный узел кластера.</span><span class="sxs-lookup"><span data-stu-id="e496f-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="e496f-125">Ниже указано соглашение об именовании головных и граничных узлов для кластера HDInsight с R Server.</span><span class="sxs-lookup"><span data-stu-id="e496f-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="e496f-126">Головной узел — `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e496f-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="e496f-127">Граничный узел — `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e496f-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="e496f-128">Подключитесь к граничному узлу кластера по протоколу SSH, используя схему именования, приведенную в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="e496f-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="e496f-129">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e496f-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e496f-130">После подключения используйте учетные данные привилегированного пользователя в кластере.</span><span class="sxs-lookup"><span data-stu-id="e496f-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="e496f-131">В сеансе SSH используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e496f-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="e496f-132">Скачайте пользовательский скрипт для установки RStudio.</span><span class="sxs-lookup"><span data-stu-id="e496f-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="e496f-133">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e496f-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="e496f-134">Измените разрешения для файла пользовательского скрипта и запустите скрипт.</span><span class="sxs-lookup"><span data-stu-id="e496f-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="e496f-135">Используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e496f-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="e496f-136">Если при создании кластера HDInsight с R Server использовался пароль SSH, можно пропустить этот шаг и перейти к следующему.</span><span class="sxs-lookup"><span data-stu-id="e496f-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="e496f-137">Если вместо него для создания кластера использовался ключ SSH, необходимо задать пароль для пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="e496f-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="e496f-138">Этот пароль понадобится при подключении к RStudio.</span><span class="sxs-lookup"><span data-stu-id="e496f-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="e496f-139">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e496f-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="e496f-140">При появлении запроса на ввод **текущего пароля Kerberos** нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="e496f-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="e496f-141">Обратите внимание, что `USERNAME` необходимо заменить именем пользователя SSH для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="e496f-142">В случае успешной установки пароля появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="e496f-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="e496f-143">Выйдите из сеанса SSH.</span><span class="sxs-lookup"><span data-stu-id="e496f-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="e496f-144">Создайте туннель SSH для кластера, сопоставив `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` в кластере HDInsight с клиентским компьютером.</span><span class="sxs-lookup"><span data-stu-id="e496f-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="e496f-145">Туннель SSH следует создать перед открытием нового сеанса браузера.</span><span class="sxs-lookup"><span data-stu-id="e496f-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="e496f-146">В клиенте Linux или Windows с [Cygwin](http://www.redhat.com/services/custom/cygwin/) откройте сеанс терминала и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e496f-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="e496f-147">Замените **USERNAME** именем пользователя SSH для кластера HDInsight, а **CLUSTERNAME** — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e496f-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="e496f-148">Можно также использовать ключ SSH, а не пароль, добавив `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="e496f-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="e496f-149">Если вы используете клиент Windows и PuTTY, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e496f-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="e496f-150">Откройте PuTTY и введите информацию о подключении.</span><span class="sxs-lookup"><span data-stu-id="e496f-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="e496f-151">В разделе **Категории** в левой части диалогового окна последовательно разверните **Подключение**, **SSH** и выберите **Туннели**.</span><span class="sxs-lookup"><span data-stu-id="e496f-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="e496f-152">Введите следующую информацию в форме **Параметры, управляющие перенаправлением портов SSH** :</span><span class="sxs-lookup"><span data-stu-id="e496f-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="e496f-153">**Порт источника** — порт на стороне клиента, трафик которого нужно перенаправлять.</span><span class="sxs-lookup"><span data-stu-id="e496f-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="e496f-154">Например, **8787**.</span><span class="sxs-lookup"><span data-stu-id="e496f-154">For example, **8787**.</span></span>
        * <span data-ttu-id="e496f-155">**Назначение** — место назначения, которое следует сопоставить с локальным клиентским компьютером.</span><span class="sxs-lookup"><span data-stu-id="e496f-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="e496f-156">Например, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="e496f-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="e496f-157">![Создание туннеля SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "создание туннеля SSH")</span><span class="sxs-lookup"><span data-stu-id="e496f-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="e496f-158">Щелкните **Добавить**, чтобы добавить параметры, а затем щелкните **Открыть**, чтобы открыть подключение SSH.</span><span class="sxs-lookup"><span data-stu-id="e496f-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="e496f-159">При появлении запроса войдите на сервер. При этом будет установлен сеанс SSH и включен туннель.</span><span class="sxs-lookup"><span data-stu-id="e496f-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="e496f-160">Откройте браузер и введите следующий URL-адрес с учетом порта, введенного для туннеля:</span><span class="sxs-lookup"><span data-stu-id="e496f-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="e496f-161">Появится запрос на ввод имени пользователя и пароля SSH для подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="e496f-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="e496f-162">Если при создании кластера использовался ключ SSH, необходимо ввести пароль, созданный в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="e496f-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="e496f-163">![Подключение к R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "создание туннеля SSH")</span><span class="sxs-lookup"><span data-stu-id="e496f-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="e496f-164">Чтобы проверить успешность установки RStudio, можно запустить тестовый скрипт, выполняющий задания MapReduce и Spark на языке R в кластере.</span><span class="sxs-lookup"><span data-stu-id="e496f-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="e496f-165">Чтобы скачать тестовый скрипт для запуска в RStudio, вернитесь в консоль SSH и введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e496f-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="e496f-166">При создании кластера Hadoop на языке R используйте эту команду:</span><span class="sxs-lookup"><span data-stu-id="e496f-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="e496f-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="e496f-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="e496f-168">При создании кластера Spark на языке R используйте эту команду:</span><span class="sxs-lookup"><span data-stu-id="e496f-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="e496f-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="e496f-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="e496f-170">В RStudio появится скачанный тестовый скрипт.</span><span class="sxs-lookup"><span data-stu-id="e496f-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="e496f-171">Дважды щелкните файл, чтобы открыть его, выделите содержимое файла и нажмите кнопку **Run** (Запустить).</span><span class="sxs-lookup"><span data-stu-id="e496f-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="e496f-172">Результаты появятся в области **Console** (Консоль).</span><span class="sxs-lookup"><span data-stu-id="e496f-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="e496f-173">![Проверка установки](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "проверка установки")</span><span class="sxs-lookup"><span data-stu-id="e496f-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="e496f-174">Еще один вариант — ввести `source(testhdi.r)` или `source(testhdi_spark.r)` для выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="e496f-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="e496f-175">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e496f-175">See also</span></span>

* [<span data-ttu-id="e496f-176">Compute context options for R Server on HDInsight clusters (Параметры контекста вычислений для R Server в кластерах HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e496f-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="e496f-177">Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e496f-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

