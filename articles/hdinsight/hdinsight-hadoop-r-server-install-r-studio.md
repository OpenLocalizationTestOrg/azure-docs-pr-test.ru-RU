---
title: "aaaInstall RStudio с сервером R в HDInsight - Azure | Документы Microsoft"
description: "Как tooinstall RStudio с сервером R в HDInsight."
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="626c8-103">Установка RStudio с R Server в HDInsight</span><span class="sxs-lookup"><span data-stu-id="626c8-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="626c8-104">В этой статье описывается, как tooinstall hello сообщества (бесплатно) версия [RStudio сервера](https://www.rstudio.com/products/rstudio-server/) на hello граничного узла кластера с помощью пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="626c8-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="626c8-105">RStudio Server предоставляет интегрированную среду разработки (IDE) на основе браузера, предназначенную для удаленных клиентов и широко используемую в Linux.</span><span class="sxs-lookup"><span data-stu-id="626c8-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="626c8-106">Для языка R в настоящее время доступно множество интегрированных сред разработки, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="626c8-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="626c8-107">[Инструменты R для Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) от корпорации Майкрософт</span><span class="sxs-lookup"><span data-stu-id="626c8-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="626c8-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="626c8-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="626c8-109">[StatET](http://www.walware.de/goto/statet) на основе Eclipse от компании Walware</span><span class="sxs-lookup"><span data-stu-id="626c8-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="626c8-110">Hello преимущество установки RStudio сервера на приветствия граничного узла из кластера HDInsight — что она обеспечивает полной интегрированной СРЕДЫ разработки hello разработки и выполнения скриптов R с R Server на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="626c8-111">Эта конфигурация может быть значительно более производительны, чем использование по умолчанию hello R консоли.</span><span class="sxs-lookup"><span data-stu-id="626c8-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="626c8-112">Hello процедуру, описанную в данной статье применяется только в том случае, если вы не выбрали tooinstall RStudio Server community edition при подготовке кластера.</span><span class="sxs-lookup"><span data-stu-id="626c8-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="626c8-113">При добавлении во время инициализации, затем tooaccess его щелкнуть hello **панели мониторинга сервера R** плитки в hello Azure портала запись для кластера, а затем в hello **R Studio Server** плитки.</span><span class="sxs-lookup"><span data-stu-id="626c8-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="626c8-114">При желании toouse hello коммерчески лицензия Pro версии RStudio Server необходимо выполнить инструкции по установке hello из [RStudio сервера](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="626c8-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="626c8-115">При использовании кластера HDInsight, для которого R был установлен при помощи hello [действия сценария R установка](hdinsight-hadoop-r-scripts-linux.md), hello шагов в этом документе не будет работать правильно, как они требуют R Server в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="626c8-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="626c8-116">Prerequisites</span></span>

* <span data-ttu-id="626c8-117">Кластер Azure HDInsight, на котором установлен R Server.</span><span class="sxs-lookup"><span data-stu-id="626c8-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="626c8-118">Инструкции см. в статье [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="626c8-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="626c8-119">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="626c8-119">An SSH client.</span></span> <span data-ttu-id="626c8-120">Для дистрибутивах Linux и Unix или Macintosh OS X, hello `ssh` команда входит в состав операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="626c8-121">Для Windows, мы рекомендуем [Cygwin](http://www.redhat.com/services/custom/cygwin/) с hello [параметр OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), или [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="626c8-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="626c8-122">Установка RStudio на кластере hello, с помощью пользовательского сценария</span><span class="sxs-lookup"><span data-stu-id="626c8-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="626c8-123">Ниже приведены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-123">Here are hello steps:</span></span>

1. <span data-ttu-id="626c8-124">Определите hello граничного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="626c8-125">Для кластера HDInsight с сервером R ниже приведен hello соглашение об именовании для головного узла и граничного узла.</span><span class="sxs-lookup"><span data-stu-id="626c8-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="626c8-126">Головной узел — `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="626c8-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="626c8-127">Граничный узел — `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="626c8-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="626c8-128">SSH в hello граничного узла кластера hello, используя шаблон именования hello, указанных на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="626c8-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="626c8-129">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="626c8-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="626c8-130">Если вы подключены, становятся привилегированного пользователя на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="626c8-131">В сеансе SSH hello используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="626c8-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="626c8-132">Загрузите пользовательский сценарий hello tooinstall RStudio.</span><span class="sxs-lookup"><span data-stu-id="626c8-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="626c8-133">Hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="626c8-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="626c8-134">Изменить разрешения hello hello пользовательский файл скрипта и запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="626c8-135">Используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="626c8-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="626c8-136">При использовании пароля SSH во время создания кластера HDInsight с сервером R, можно пропустить этот шаг и продолжить toohello Далее.</span><span class="sxs-lookup"><span data-stu-id="626c8-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="626c8-137">При использовании ключа SSH вместо toocreate hello кластера, необходимо задать пароль для пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="626c8-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="626c8-138">Этот пароль необходимо при подключении tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="626c8-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="626c8-139">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="626c8-140">При появлении запроса на ввод **текущего пароля Kerberos** нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="626c8-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="626c8-141">Обратите внимание, что `USERNAME` необходимо заменить именем пользователя SSH для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="626c8-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="626c8-142">Если пароль успешно установлен, вы увидите hello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="626c8-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="626c8-143">Завершите сеанс SSH hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="626c8-144">Создание кластера toohello туннель SSH, сопоставляя `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello HDInsight кластера toohello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="626c8-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="626c8-145">Туннель SSH следует создать перед открытием нового сеанса браузера.</span><span class="sxs-lookup"><span data-stu-id="626c8-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="626c8-146">На стороне клиента Linux или клиента Windows с [Cygwin](http://www.redhat.com/services/custom/cygwin/), откройте сеанс терминала и использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="626c8-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="626c8-147">Замените **USERNAME** пользователем SSH для кластера HDInsight и замените **CLUSTERNAME** с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="626c8-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="626c8-148">Можно также использовать ключ SSH, а не пароль, добавив `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="626c8-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="626c8-149">Если вы используете клиент Windows и PuTTY, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="626c8-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="626c8-150">Откройте PuTTY и введите информацию о подключении.</span><span class="sxs-lookup"><span data-stu-id="626c8-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="626c8-151">В hello **категории** toohello раздел левой части диалогового окна hello, разверните **подключения**, разверните **SSH**и выберите **туннели**.</span><span class="sxs-lookup"><span data-stu-id="626c8-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="626c8-152">Укажите следующую информацию на hello hello **перенаправление портов параметры, управляющие SSH** формы:</span><span class="sxs-lookup"><span data-stu-id="626c8-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="626c8-153">**Порт источника** -порт на приветствия клиента обратиться в tooforward hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="626c8-154">Например, **8787**.</span><span class="sxs-lookup"><span data-stu-id="626c8-154">For example, **8787**.</span></span>
        * <span data-ttu-id="626c8-155">**Назначение** - hello назначения, который должен быть сопоставлен toohello локальный клиентский компьютер.</span><span class="sxs-lookup"><span data-stu-id="626c8-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="626c8-156">Например, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="626c8-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="626c8-157">![Создание туннеля SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "создание туннеля SSH")</span><span class="sxs-lookup"><span data-stu-id="626c8-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="626c8-158">Нажмите кнопку **добавить** tooadd hello параметры и нажмите кнопку **откройте** tooopen SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="626c8-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="626c8-159">При появлении запроса выполните вход tooestablish сервера toohello туннель SSH сеанса и включить hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="626c8-160">Откройте веб-браузер и введите URL-адреса учетом порта hello, введенное для hello туннеля hello:</span><span class="sxs-lookup"><span data-stu-id="626c8-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="626c8-161">Все запрашиваемые tooenter hello SSH имя пользователя и пароль tooconnect toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="626c8-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="626c8-162">Если вы использовали SSH-ключ при создании кластера hello, необходимо ввести пароль hello, созданный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="626c8-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="626c8-163">![Подключение tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "создать туннель SSH")</span><span class="sxs-lookup"><span data-stu-id="626c8-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="626c8-164">tootest ли hello RStudio установки выполнена успешно, можно запустить тестовый сценарий, который выполняется на основе R задания MapReduce и Spark на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="626c8-165">toorun toodownload hello тестового скрипта в RStudio, вернитесь к предыдущему окну консоли SSH toohello и введите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="626c8-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="626c8-166">При создании кластера Hadoop на языке R используйте эту команду:</span><span class="sxs-lookup"><span data-stu-id="626c8-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="626c8-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="626c8-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="626c8-168">При создании кластера Spark на языке R используйте эту команду:</span><span class="sxs-lookup"><span data-stu-id="626c8-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="626c8-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="626c8-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="626c8-170">В RStudio просмотреть тестовый сценарий, который вы загрузили hello.</span><span class="sxs-lookup"><span data-stu-id="626c8-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="626c8-171">Дважды щелкните tooopen файл hello, выберите hello содержимое файла hello и нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="626c8-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="626c8-172">Вы должны увидеть результаты hello в hello **консоли** панели:</span><span class="sxs-lookup"><span data-stu-id="626c8-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="626c8-173">![Проверьте установку hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "протестировать установку hello")</span><span class="sxs-lookup"><span data-stu-id="626c8-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="626c8-174">Можно было бы tootype `source(testhdi.r)` или `source(testhdi_spark.r)` tooexecute hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="626c8-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="626c8-175">См. также</span><span class="sxs-lookup"><span data-stu-id="626c8-175">See also</span></span>

* [<span data-ttu-id="626c8-176">Compute context options for R Server on HDInsight clusters (Параметры контекста вычислений для R Server в кластерах HDInsight)</span><span class="sxs-lookup"><span data-stu-id="626c8-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="626c8-177">Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="626c8-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

