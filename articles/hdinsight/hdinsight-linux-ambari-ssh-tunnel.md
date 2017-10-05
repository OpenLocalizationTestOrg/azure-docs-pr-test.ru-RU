---
title: "Использование туннелирования SSH для доступа к Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как безопасно просматривать веб-ресурсы, размещенные на узлах HDInsight под управлением Linux, с помощью туннеля SSH."
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="3775d-103">Использование туннелирования SSH для доступа к пользовательскому веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим пользовательским веб-интерфейсам</span><span class="sxs-lookup"><span data-stu-id="3775d-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="3775d-104">Кластеры HDInsight под управлением Linux предоставляют доступ к веб-интерфейсу Ambari через Интернет, однако при этом доступны не все функции веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3775d-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="3775d-105">Это относится, например, к веб-интерфейсу других служб, которые доступны через Ambari.</span><span class="sxs-lookup"><span data-stu-id="3775d-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="3775d-106">Чтобы получить доступ ко всем функциям веб-интерфейса Ambari, необходимо настроить туннель SSH к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="3775d-107">Причины для использования туннеля SSH</span><span class="sxs-lookup"><span data-stu-id="3775d-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="3775d-108">Некоторые меню в Ambari работают только через туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="3775d-109">Для этих меню используются веб-сайты и службы, выполняющиеся на узлах других типов, например рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="3775d-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="3775d-110">Часто эти веб-сайты не защищены, поэтому небезопасно открывать прямой доступ к ним через Интернет.</span><span class="sxs-lookup"><span data-stu-id="3775d-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="3775d-111">Туннель SSH требуется для следующих пользовательских веб-интерфейсов:</span><span class="sxs-lookup"><span data-stu-id="3775d-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="3775d-112">Журнал заданий</span><span class="sxs-lookup"><span data-stu-id="3775d-112">JobHistory</span></span>
* <span data-ttu-id="3775d-113">узел имен;</span><span class="sxs-lookup"><span data-stu-id="3775d-113">NameNode</span></span>
* <span data-ttu-id="3775d-114">стеки потоков;</span><span class="sxs-lookup"><span data-stu-id="3775d-114">Thread Stacks</span></span>
* <span data-ttu-id="3775d-115">веб-интерфейс Oozie</span><span class="sxs-lookup"><span data-stu-id="3775d-115">Oozie web UI</span></span>
* <span data-ttu-id="3775d-116">веб-интерфейс главного узла и журналов HBase</span><span class="sxs-lookup"><span data-stu-id="3775d-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="3775d-117">При использовании действий сценариев для настройки кластера туннель SSH будет необходим для всех служб и программ, которые вы установили для доступа к веб-интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="3775d-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="3775d-118">Например, если вы установили Hue с помощью действия сценария, для доступа к веб-интерфейсу Hue потребуется туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3775d-119">Если у вас есть прямой доступ к HDInsight через виртуальную сеть, то вам не нужно использовать туннели SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="3775d-120">Пример прямого доступа к HDInsight через виртуальную сеть см. в статье о [подключении HDInsight к локальной сети](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="3775d-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="3775d-121">Что такое туннель SSH?</span><span class="sxs-lookup"><span data-stu-id="3775d-121">What is an SSH tunnel</span></span>

<span data-ttu-id="3775d-122">[Туннелирование Secure Shell (SSH)](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) позволяет направлять трафик, отправляемый на порт локальной рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="3775d-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="3775d-123">Трафик направляется через SSH-подключение на головной узел кластера HDInsight,</span><span class="sxs-lookup"><span data-stu-id="3775d-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="3775d-124">на котором запрос разрешается так же, как если бы он был создан на головном узле.</span><span class="sxs-lookup"><span data-stu-id="3775d-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="3775d-125">Ответ рабочей станции отправляется обратно через туннель.</span><span class="sxs-lookup"><span data-stu-id="3775d-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3775d-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3775d-126">Prerequisites</span></span>

* <span data-ttu-id="3775d-127">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-127">An SSH client.</span></span> <span data-ttu-id="3775d-128">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3775d-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="3775d-129">Веб-браузер, который можно настроить на использование прокси-сервера SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="3775d-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="3775d-130">Встроенная в Windows поддержка прокси-сервера SOCKS не применяется к SOCKS5 и не работает при выполнении действий в этом документе.</span><span class="sxs-lookup"><span data-stu-id="3775d-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="3775d-131">Следующие браузеры используют параметры прокси-сервера Windows и в настоящее время не будут работать при выполнении действий в этом документе.</span><span class="sxs-lookup"><span data-stu-id="3775d-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="3775d-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="3775d-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="3775d-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="3775d-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="3775d-134">Google Chrome также использует параметры прокси-сервера Windows.</span><span class="sxs-lookup"><span data-stu-id="3775d-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="3775d-135">Но можно установить расширения, которые поддерживают SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="3775d-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="3775d-136">Рекомендуется использовать [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="3775d-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="3775d-137"><a name="usessh"></a>Создание туннеля с помощью команды SSH</span><span class="sxs-lookup"><span data-stu-id="3775d-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="3775d-138">Используйте следующую команду для создания туннеля SSH с помощью команды `ssh` .</span><span class="sxs-lookup"><span data-stu-id="3775d-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="3775d-139">Замените **USERNAME** именем пользователя SSH для кластера HDInsight, а **CLUSTERNAME** — именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3775d-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="3775d-140">Эта команда создает подключение, через которое направляется трафик, поступающий на локальный порт 9876, в кластер по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="3775d-141">Доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="3775d-141">The options are:</span></span>

* <span data-ttu-id="3775d-142">**D 9876** — локальный порт, используемый для направления трафика через туннель;</span><span class="sxs-lookup"><span data-stu-id="3775d-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="3775d-143">**C** — сжатие всех данных, так как веб-трафик преимущественно состоит из текста;</span><span class="sxs-lookup"><span data-stu-id="3775d-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="3775d-144">**2** — принудительная попытка использовать только протокол SSH версии 2;</span><span class="sxs-lookup"><span data-stu-id="3775d-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="3775d-145">**q** — тихий режим;</span><span class="sxs-lookup"><span data-stu-id="3775d-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="3775d-146">**T** — отключение распределения псевдотелетайпа, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="3775d-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="3775d-147">**n** — предотвращение считывания с STDIN, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="3775d-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="3775d-148">**N** — запрет на выполнение удаленной команды, так как выполняется только перенаправление порта;</span><span class="sxs-lookup"><span data-stu-id="3775d-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="3775d-149">**f** — выполнение в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="3775d-149">**f** - Run in the background.</span></span>

<span data-ttu-id="3775d-150">После завершения команды трафик, отправленный на порт 9876 локального компьютера, будет направляться на головной узел кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="3775d-151"><a name="useputty"></a>Создание туннеля с помощью PuTTY</span><span class="sxs-lookup"><span data-stu-id="3775d-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="3775d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) — это графический клиент SSH для Windows.</span><span class="sxs-lookup"><span data-stu-id="3775d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="3775d-153">Для создания туннеля SSH с помощью PuTTY выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3775d-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="3775d-154">Откройте PuTTY и введите информацию о подключении.</span><span class="sxs-lookup"><span data-stu-id="3775d-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="3775d-155">Если вы не работали с PuTTY, ознакомьтесь с [документацией по PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="3775d-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="3775d-156">В разделе **Категории** в левой части диалогового окна последовательно разверните **Подключение**, **SSH** и выберите **Туннели**.</span><span class="sxs-lookup"><span data-stu-id="3775d-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="3775d-157">Введите следующую информацию в форме **Параметры, управляющие перенаправлением портов SSH** :</span><span class="sxs-lookup"><span data-stu-id="3775d-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="3775d-158">**Порт источника** — порт на стороне клиента, трафик которого нужно перенаправлять.</span><span class="sxs-lookup"><span data-stu-id="3775d-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="3775d-159">Например, **9876**.</span><span class="sxs-lookup"><span data-stu-id="3775d-159">For example, **9876**.</span></span>

   * <span data-ttu-id="3775d-160">**Назначение** — адрес SSH для кластера HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="3775d-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3775d-161">Например, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="3775d-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="3775d-162">**Динамическая** — включает динамическую маршрутизацию прокси-сервера SOCKS.</span><span class="sxs-lookup"><span data-stu-id="3775d-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![изображение параметров туннелирования](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="3775d-164">Щелкните **Добавить**, чтобы добавить параметры, а затем щелкните **Открыть**, чтобы открыть подключение SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="3775d-165">При появлении запроса войдите на сервер.</span><span class="sxs-lookup"><span data-stu-id="3775d-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="3775d-166">Использование туннеля из браузера</span><span class="sxs-lookup"><span data-stu-id="3775d-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3775d-167">Для действий, описанных в этом разделе, используется браузер FireFox, так как предоставляет те же параметры прокси-сервера на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="3775d-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="3775d-168">Для других современных браузеров, например Google Chrome, может потребоваться расширение, например FoxyProxy, для работы с туннелем.</span><span class="sxs-lookup"><span data-stu-id="3775d-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="3775d-169">Настроить браузер для использования **localhost** и порта, использованного при создании туннеля, в качестве прокси-сервера **SOCKS 5**.</span><span class="sxs-lookup"><span data-stu-id="3775d-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="3775d-170">Вот как выглядят параметры Firefox.</span><span class="sxs-lookup"><span data-stu-id="3775d-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="3775d-171">Если используется порт, отличный от 9876, измените номер порта соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="3775d-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![изображение параметров Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="3775d-173">Если выбрать параметр **Remote DNS** (Удаленная служба DNS), то запросы службы доменных имен (DNS) будут разрешаться с помощью кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3775d-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="3775d-174">Этот параметр разрешает запросы DNS с помощью головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="3775d-175">Чтобы проверить, работает ли туннель, зайдите на сайт [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="3775d-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="3775d-176">Возвращаемый IP-адрес должен быть адресом, который используется центром обработки данных Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3775d-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="3775d-177">Проверка для веб-интерфейса Ambari</span><span class="sxs-lookup"><span data-stu-id="3775d-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="3775d-178">После настройки кластера выполните следующие действия, чтобы удостовериться, что веб-интерфейсы служб доступны из веб-интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="3775d-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="3775d-179">В браузере перейдите по адресу: http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="3775d-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="3775d-180">Адрес `headnodehost` отправляется через туннель в кластер и преобразовывается в головной узел, на котором выполняется Ambari.</span><span class="sxs-lookup"><span data-stu-id="3775d-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="3775d-181">При появлении запроса введите имя пользователя (admin) и пароль учетной записи администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="3775d-182">Веб-интерфейс Ambari может потребовать повторного ввода имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="3775d-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="3775d-183">В этом случае повторно введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="3775d-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3775d-184">При использовании адреса http://headnodehost:8080 для подключения к кластеру вы подключаетесь через туннель.</span><span class="sxs-lookup"><span data-stu-id="3775d-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="3775d-185">Безопасность обмена данными обеспечивает туннель SSH, а не протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3775d-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="3775d-186">Для подключения через Интернет по протоколу HTTPS используйте https://CLUSTERNAME.azurehdinsight.net, где **имя_кластера** — имя кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="3775d-187">В веб-интерфейсе Ambari выберите HDFS в списке в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="3775d-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Изображение с выбранным пунктом HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="3775d-189">После появления информации о службе HDFS выберите **Быстрые ссылки**.</span><span class="sxs-lookup"><span data-stu-id="3775d-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="3775d-190">Появится список головных узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="3775d-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="3775d-191">Выберите один из головных узлов, а затем выберите **NameNode UI**(Пользовательский интерфейс NameNode).</span><span class="sxs-lookup"><span data-stu-id="3775d-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Изображение с развернутым меню "Быстрые ссылки"](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="3775d-193">При выборе меню __Быстрые ссылки__ может появиться индикатор ожидания.</span><span class="sxs-lookup"><span data-stu-id="3775d-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="3775d-194">Это может произойти, если подключение к Интернету медленное.</span><span class="sxs-lookup"><span data-stu-id="3775d-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="3775d-195">Подождите одну-две минуты для получения данных с сервера, а затем повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="3775d-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="3775d-196">Некоторые записи в меню **Быстрые ссылки** могут быть обрезаны правым краем экрана.</span><span class="sxs-lookup"><span data-stu-id="3775d-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="3775d-197">В этом случае разверните меню с помощью мыши и используйте клавишу со стрелкой вправо, чтобы прокрутить экран вправо и увидеть остальную часть меню.</span><span class="sxs-lookup"><span data-stu-id="3775d-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="3775d-198">Откроется страница, аналогичная следующей:</span><span class="sxs-lookup"><span data-stu-id="3775d-198">A page similar to the following image is displayed:</span></span>

    ![Изображение пользовательского интерфейса NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="3775d-200">Обратите внимание на URL-адрес этой страницы. Он должен иметь вид **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="3775d-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="3775d-201">Этот URI использует полное внутреннее доменное имя узла (FQDN), и он доступен только при использовании туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="3775d-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3775d-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3775d-202">Next steps</span></span>

<span data-ttu-id="3775d-203">Теперь, когда вы узнали, как создать и использовать туннель SSH, просмотрите другие способы использования Ambari в следующем документе:</span><span class="sxs-lookup"><span data-stu-id="3775d-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="3775d-204">Управление кластерами HDInsight с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="3775d-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="3775d-205">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3775d-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

