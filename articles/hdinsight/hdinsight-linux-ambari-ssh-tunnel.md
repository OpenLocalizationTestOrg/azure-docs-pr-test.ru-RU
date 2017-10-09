---
title: "aaaUse SSH туннелирования tooaccess Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse toosecurely туннель SSH Обзор веб-ресурсов, размещенных на узлах под управлением Linux HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="0d047-103">Использовать туннелирование SSH tooaccess Ambari web пользовательского интерфейса, JobHistory, NameNode, Oozie и других веб-интерфейсы пользователя</span><span class="sxs-lookup"><span data-stu-id="0d047-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="0d047-104">Кластеры HDInsight под управлением Linux предоставления пользовательского интерфейса web tooAmbari доступ через Интернет hello, но некоторые функции hello пользовательского интерфейса не имеют.</span><span class="sxs-lookup"><span data-stu-id="0d047-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="0d047-105">Например hello веб-интерфейса для других служб, подключаемых через Ambari.</span><span class="sxs-lookup"><span data-stu-id="0d047-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="0d047-106">Для обеспечения полной функциональности hello Ambari web пользовательского интерфейса необходимо использовать head кластера toohello туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="0d047-107">Причины для использования туннеля SSH</span><span class="sxs-lookup"><span data-stu-id="0d047-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="0d047-108">Некоторые из меню hello в Ambari работают только через туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="0d047-109">Для этих меню используются веб-сайты и службы, выполняющиеся на узлах других типов, например рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="0d047-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="0d047-110">Часто эти веб-узлы не защищены, поэтому не предоставляют безопасные toodirectly их на hello Интернет.</span><span class="sxs-lookup"><span data-stu-id="0d047-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="0d047-111">Привет, следуя пользовательских веб-интерфейсов требуется туннель SSH:</span><span class="sxs-lookup"><span data-stu-id="0d047-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="0d047-112">Журнал заданий</span><span class="sxs-lookup"><span data-stu-id="0d047-112">JobHistory</span></span>
* <span data-ttu-id="0d047-113">узел имен;</span><span class="sxs-lookup"><span data-stu-id="0d047-113">NameNode</span></span>
* <span data-ttu-id="0d047-114">стеки потоков;</span><span class="sxs-lookup"><span data-stu-id="0d047-114">Thread Stacks</span></span>
* <span data-ttu-id="0d047-115">веб-интерфейс Oozie</span><span class="sxs-lookup"><span data-stu-id="0d047-115">Oozie web UI</span></span>
* <span data-ttu-id="0d047-116">веб-интерфейс главного узла и журналов HBase</span><span class="sxs-lookup"><span data-stu-id="0d047-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="0d047-117">При использовании действия скрипта toocustomize кластера никаких служб или программ, установке, предоставляющих веб-интерфейса требуется туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="0d047-118">Например при установке оттенка с помощью действия сценария, необходимо использовать SSH туннеля tooaccess hello оттенка пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0d047-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d047-119">Если у вас есть tooHDInsight прямой доступ через виртуальную сеть, не обязательно toouse туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="0d047-120">Пример прямого доступа к HDInsight через виртуальную сеть, в разделе hello [HDInsight подключения tooyour локальной сети](connect-on-premises-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="0d047-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="0d047-121">Что такое туннель SSH?</span><span class="sxs-lookup"><span data-stu-id="0d047-121">What is an SSH tunnel</span></span>

<span data-ttu-id="0d047-122">[Secure Shell (SSH) туннелирование](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) направляет трафик tooa порт на локальной рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="0d047-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="0d047-123">Hello трафик направляется через SSH подключения tooyour HDInsight головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="0d047-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="0d047-124">запрос Hello определяется, как если бы она была создана на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="0d047-125">ответ Hello направляется обратно через туннель hello tooyour-рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="0d047-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d047-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0d047-126">Prerequisites</span></span>

* <span data-ttu-id="0d047-127">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-127">An SSH client.</span></span> <span data-ttu-id="0d047-128">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0d047-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="0d047-129">Веб-браузер, может быть настроен прокси-серверов SOCKS5 toouse.</span><span class="sxs-lookup"><span data-stu-id="0d047-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0d047-130">Поддержка прокси-сервера SOCKS Hello, встроенная в Windows не поддерживает SOCKS5 и не работает с hello в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="0d047-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="0d047-131">Hello следующие браузеры используют параметры прокси-сервера Windows и не в настоящее время работают с hello в данном пошаговом руководстве:</span><span class="sxs-lookup"><span data-stu-id="0d047-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="0d047-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="0d047-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="0d047-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="0d047-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="0d047-134">Google Chrome также зависит от параметров прокси-сервера Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="0d047-135">Но можно установить расширения, которые поддерживают SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="0d047-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="0d047-136">Рекомендуется использовать [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="0d047-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="0d047-137"><a name="usessh"></a>Создает туннель, с помощью команды SSH hello</span><span class="sxs-lookup"><span data-stu-id="0d047-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="0d047-138">Используйте hello следующая команда toocreate туннель SSH, с помощью hello `ssh` команды.</span><span class="sxs-lookup"><span data-stu-id="0d047-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="0d047-139">Замените **USERNAME** пользователем SSH для кластера HDInsight и замените **CLUSTERNAME** с hello имя кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0d047-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="0d047-140">Эта команда создает подключение, которое направляет трафик toolocal порт 9876 toohello кластера через SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="0d047-141">доступны следующие параметры Hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-141">hello options are:</span></span>

* <span data-ttu-id="0d047-142">**D 9876** -hello локальный порт, который перенаправляет трафик через туннель hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="0d047-143">**C** — сжатие всех данных, так как веб-трафик преимущественно состоит из текста;</span><span class="sxs-lookup"><span data-stu-id="0d047-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="0d047-144">**2** -force SSH tootry протокол версии 2 только.</span><span class="sxs-lookup"><span data-stu-id="0d047-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="0d047-145">**q** — тихий режим;</span><span class="sxs-lookup"><span data-stu-id="0d047-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="0d047-146">**T** — отключение распределения псевдотелетайпа, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="0d047-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="0d047-147">**n** — предотвращение считывания с STDIN, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="0d047-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="0d047-148">**N** — запрет на выполнение удаленной команды, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="0d047-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="0d047-149">**f** -выполняются в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="0d047-150">После завершения выполнения команды hello tooport трафик 9876 на локальном компьютере hello является перенаправленное toohello головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="0d047-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="0d047-151"><a name="useputty"></a>Создание туннеля с помощью PuTTY</span><span class="sxs-lookup"><span data-stu-id="0d047-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="0d047-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) — это графический клиент SSH для Windows.</span><span class="sxs-lookup"><span data-stu-id="0d047-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="0d047-153">Используйте следующие шаги toocreate туннель SSH, с помощью PuTTY hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="0d047-154">Откройте PuTTY и введите информацию о подключении.</span><span class="sxs-lookup"><span data-stu-id="0d047-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="0d047-155">Если вы не знакомы с PuTTY, см. раздел hello [PuTTY документации (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="0d047-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="0d047-156">В hello **категории** toohello раздел левой части диалогового окна hello, разверните **подключения**, разверните **SSH**и выберите **туннели**.</span><span class="sxs-lookup"><span data-stu-id="0d047-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="0d047-157">Укажите следующую информацию на hello hello **перенаправление портов параметры, управляющие SSH** формы:</span><span class="sxs-lookup"><span data-stu-id="0d047-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="0d047-158">**Порт источника** -порт на приветствия клиента обратиться в tooforward hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="0d047-159">Например, **9876**.</span><span class="sxs-lookup"><span data-stu-id="0d047-159">For example, **9876**.</span></span>

   * <span data-ttu-id="0d047-160">**Назначение** -hello SSH-адрес для кластера HDInsight под управлением Linux hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0d047-161">Например, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="0d047-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="0d047-162">**Динамическая** — включает динамическую маршрутизацию прокси-сервера SOCKS.</span><span class="sxs-lookup"><span data-stu-id="0d047-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![изображение параметров туннелирования](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="0d047-164">Нажмите кнопку **добавить** tooadd hello параметры и нажмите кнопку **откройте** tooopen SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="0d047-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="0d047-165">При появлении запроса выполните вход toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="0d047-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="0d047-166">Используйте туннеля hello из браузера</span><span class="sxs-lookup"><span data-stu-id="0d047-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d047-167">Hello шагов в hello используйте этот раздел браузера Mozilla FireFox, поскольку она обеспечивает hello одинаковые параметры прокси-сервера на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="0d047-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="0d047-168">Другими современными браузерами, например Google Chrome, может потребоваться расширение, например toowork FoxyProxy с hello туннеля.</span><span class="sxs-lookup"><span data-stu-id="0d047-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="0d047-169">Настройка обозревателя toouse hello **localhost** и hello порт, который использовался при создании туннеля hello как **SOCKS v5** прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0d047-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="0d047-170">Ниже показано, как выглядят параметры Firefox hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="0d047-171">Если используется другой порт, чем 9876 измените toohello порт hello тот, который используется:</span><span class="sxs-lookup"><span data-stu-id="0d047-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![изображение параметров Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="0d047-173">При выборе **удаленного DNS** разрешает запросы доменных имен (DNS) с помощью hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d047-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="0d047-174">Этот параметр разрешает DNS с помощью hello головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="0d047-175">Убедитесь, что туннель hello работает, перейдя по адресу сайта, таких как [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="0d047-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="0d047-176">Hello IP возвращается один используемого центра обработки данных Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="0d047-177">Проверка для веб-интерфейса Ambari</span><span class="sxs-lookup"><span data-stu-id="0d047-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="0d047-178">После установления hello кластера используйте следующие шаги tooverify из hello Ambari Web доступен веб-службы пользовательских интерфейсов hello:</span><span class="sxs-lookup"><span data-stu-id="0d047-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="0d047-179">В браузере перейдите toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="0d047-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="0d047-180">Hello `headnodehost` адрес передаются через hello туннеля toohello кластера и разрешить toohello головному узлу, на котором Ambari работает на.</span><span class="sxs-lookup"><span data-stu-id="0d047-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="0d047-181">При появлении запроса введите имя пользователя администратора hello (администратор) и пароль для кластера.</span><span class="sxs-lookup"><span data-stu-id="0d047-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="0d047-182">Может потребоваться еще раз, hello Ambari web пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0d047-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="0d047-183">В этом случае введите сведения hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0d047-184">При использовании hello http://headnodehost:8080 адрес tooconnect toohello кластера, при подключении через туннель hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="0d047-185">Безопасность обмена данными с использованием туннеля SSH hello вместо HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0d047-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="0d047-186">tooconnect более hello Интернет с использованием HTTPS, используйте https://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — имя кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="0d047-187">Hello Ambari веб-интерфейса выберите из списка hello hello левой стороны страницы приветствия HDFS.</span><span class="sxs-lookup"><span data-stu-id="0d047-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Изображение с выбранным пунктом HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="0d047-189">При отображении hello сведения о службе HDFS, выберите **быстрые ссылки**.</span><span class="sxs-lookup"><span data-stu-id="0d047-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="0d047-190">Появится список головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0d047-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="0d047-191">Выберите один из головного узла hello, а затем выберите **NameNode пользовательского интерфейса**.</span><span class="sxs-lookup"><span data-stu-id="0d047-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Развернуть образ с меню QuickLinks hello](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="0d047-193">При выборе меню __Быстрые ссылки__ может появиться индикатор ожидания.</span><span class="sxs-lookup"><span data-stu-id="0d047-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="0d047-194">Это может произойти, если подключение к Интернету медленное.</span><span class="sxs-lookup"><span data-stu-id="0d047-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="0d047-195">Подождите минуту или две для hello toobe данных, полученных с сервера hello, а затем повторите попытку hello список.</span><span class="sxs-lookup"><span data-stu-id="0d047-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="0d047-196">Некоторые записи в hello **быстрые ссылки** меню может быть обрезана hello правой части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="0d047-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="0d047-197">В этом случае разверните меню hello, с помощью мыши и использовать hello со стрелкой вправо ключа tooscroll hello экрана toohello правой toosee hello rest меню «hello».</span><span class="sxs-lookup"><span data-stu-id="0d047-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="0d047-198">Отображается примерно toohello страницы, после изображения.</span><span class="sxs-lookup"><span data-stu-id="0d047-198">A page similar toohello following image is displayed:</span></span>

    ![Изображение hello NameNode пользовательского интерфейса](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="0d047-200">Обратите внимание, hello URL-адрес для этой страницы; он должен выглядеть слишком**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088 и кластером**.</span><span class="sxs-lookup"><span data-stu-id="0d047-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="0d047-201">Этот URI используется hello внутреннее полное доменное имя (FQDN) узла hello и доступен только при использовании туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="0d047-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d047-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d047-202">Next steps</span></span>

<span data-ttu-id="0d047-203">Теперь, когда вы узнали, как toocreate и используйте туннель SSH см. следующий документ для других способов toouse Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="0d047-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="0d047-204">Управление кластерами HDInsight с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="0d047-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="0d047-205">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0d047-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

