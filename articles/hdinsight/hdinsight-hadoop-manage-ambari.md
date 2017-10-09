---
title: "aaaMonitor и управлять ими с помощью Ambari веб-интерфейса Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Ambari toomonitor кластеров HDInsight под управлением Linux и управление ими. В этом документе вы узнаете, как кластеры hello toouse Ambari веб-интерфейса, включенных в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="21c8d-104">Управление кластерами HDInsight с помощью hello Ambari веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="21c8d-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="21c8d-105">Apache Ambari упрощает управление hello и мониторинг кластера Hadoop, предоставляя простой toouse веб-интерфейса пользователя и REST API.</span><span class="sxs-lookup"><span data-stu-id="21c8d-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="21c8d-106">Ambari включается в кластерах HDInsight под управлением Linux, а — hello используется toomonitor кластера и изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21c8d-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="21c8d-107">В этом документе вы узнаете, как toouse hello Ambari веб-интерфейса пользователя с кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c8d-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="21c8d-108"><a id="whatis"></a>Что такое Ambari</span><span class="sxs-lookup"><span data-stu-id="21c8d-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="21c8d-109">[Apache Ambari](http://ambari.apache.org) упрощает управление Hadoop, предоставляя простой в использовании веб-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="21c8d-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="21c8d-110">Ambari можно использовать для создания и отслеживания кластеров Hadoop, а также для управления ими.</span><span class="sxs-lookup"><span data-stu-id="21c8d-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="21c8d-111">Разработчики могут интегрировать эти возможности в свои приложения с помощью hello [API-интерфейс REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="21c8d-112">по умолчанию с кластерами HDInsight, использующих операционной системы Linux hello предоставляется Hello Ambari веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="21c8d-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c8d-113">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="21c8d-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="21c8d-114">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="21c8d-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="21c8d-115">Соединение</span><span class="sxs-lookup"><span data-stu-id="21c8d-115">Connectivity</span></span>

<span data-ttu-id="21c8d-116">Hello Ambari веб-интерфейса можно найти в кластер HDInsight в HTTPS://CLUSTERNAME.azurehdidnsight.net, где **CLUSTERNAME** — hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="21c8d-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c8d-117">Подключение tooAmbari на HDInsight требуется протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="21c8d-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="21c8d-118">При запросе проверки подлинности следует используйте имя учетной записи администратора hello и пароль, указанный при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="21c8d-119">Туннель SSH (прокси-сервер)</span><span class="sxs-lookup"><span data-stu-id="21c8d-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="21c8d-120">Хотя Ambari для кластера доступен непосредственно через Интернет hello, некоторые ссылки из hello Ambari веб-интерфейса (например, toohello JobTracker) не предоставляются в hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="21c8d-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="21c8d-121">tooaccess этих служб, необходимо создать туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="21c8d-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="21c8d-122">Дополнительные сведения см. в статье [Использование туннелирования SSH с для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="21c8d-123">Веб-интерфейс Ambari</span><span class="sxs-lookup"><span data-stu-id="21c8d-123">Ambari Web UI</span></span>

<span data-ttu-id="21c8d-124">При подключении toohello Ambari веб-интерфейса пользователя, все запрашиваемые tooauthenticate toohello страницы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="21c8d-125">Используйте администратор кластера hello (по умолчанию администратора) и пароль, используемый во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="21c8d-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="21c8d-126">При открытии страницы приветствия, обратите внимание, строка hello вверху hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="21c8d-127">Эта панель содержит hello следующие сведения и элементы управления:</span><span class="sxs-lookup"><span data-stu-id="21c8d-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="21c8d-129">**Эмблема Ambari** -hello откроется панель мониторинга, которая может быть кластера используется toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="21c8d-130">**Кластер ops # имя** -hello число текущих Ambari операций.</span><span class="sxs-lookup"><span data-stu-id="21c8d-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="21c8d-131">Выберите имя кластера hello или **# ops** отображает список фоновые операции.</span><span class="sxs-lookup"><span data-stu-id="21c8d-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="21c8d-132">**оповещения #** -отображает предупреждения и критические оповещения, если для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="21c8d-133">**Панель мониторинга** -панели мониторинга отображает hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="21c8d-134">**Службы** -информацию и параметры конфигурации для служб hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="21c8d-135">**Узлы** -информацию и параметры конфигурации для hello узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="21c8d-136">**Оповещения** — журнал с информацией, предупреждениями и критическими оповещениями.</span><span class="sxs-lookup"><span data-stu-id="21c8d-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="21c8d-137">**Администратор** -программного стека или служб, установленных на кластер hello, сведения об учетной записи службы и безопасности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="21c8d-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="21c8d-138">**Кнопка «Администратор»** — управление Ambari, параметры пользователя и выход.</span><span class="sxs-lookup"><span data-stu-id="21c8d-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="21c8d-139">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="21c8d-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="21c8d-140">Оповещения</span><span class="sxs-lookup"><span data-stu-id="21c8d-140">Alerts</span></span>

<span data-ttu-id="21c8d-141">Hello следующий список содержит hello общих состояний используемые Ambari.</span><span class="sxs-lookup"><span data-stu-id="21c8d-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="21c8d-142">**ОК;**</span><span class="sxs-lookup"><span data-stu-id="21c8d-142">**OK**</span></span>
* <span data-ttu-id="21c8d-143">**Предупреждение;**</span><span class="sxs-lookup"><span data-stu-id="21c8d-143">**Warning**</span></span>
* <span data-ttu-id="21c8d-144">**КРИТИЧЕСКИЙ;**</span><span class="sxs-lookup"><span data-stu-id="21c8d-144">**CRITICAL**</span></span>
* <span data-ttu-id="21c8d-145">**НЕИЗВЕСТНО.**</span><span class="sxs-lookup"><span data-stu-id="21c8d-145">**UNKNOWN**</span></span>

<span data-ttu-id="21c8d-146">Предупреждения, отличный от **ОК** вызвать hello **# оповещения** входа вверху hello hello страницы toodisplay hello число оповещений.</span><span class="sxs-lookup"><span data-stu-id="21c8d-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="21c8d-147">При выборе этой записи отображаются оповещения hello и их состояние.</span><span class="sxs-lookup"><span data-stu-id="21c8d-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="21c8d-148">Предупреждения организованы в несколько групп по умолчанию, которые могут быть просмотрены при помощи hello **оповещения** страницы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![страница «Оповещения»](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="21c8d-150">Hello группы можно управлять с помощью hello **действия** , выберите в меню **Управление группами предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="21c8d-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![диалоговое окно «Управление группами оповещений»](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="21c8d-152">Можно управлять методов и создания уведомлений из hello **действия** меню, выбрав __управление уведомления предупреждение__.</span><span class="sxs-lookup"><span data-stu-id="21c8d-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="21c8d-153">Отображаются все текущие уведомления.</span><span class="sxs-lookup"><span data-stu-id="21c8d-153">Any current notifications are displayed.</span></span> <span data-ttu-id="21c8d-154">Здесь можно также создавать уведомления.</span><span class="sxs-lookup"><span data-stu-id="21c8d-154">You can also create notifications from here.</span></span> <span data-ttu-id="21c8d-155">Уведомления можно отправлять по **электронной почте** или **протоколу SNMP** при возникновении определенного сочетания оповещения и уровня серьезности.</span><span class="sxs-lookup"><span data-stu-id="21c8d-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="21c8d-156">Например, можно отправить сообщение электронной почты, если какие-либо предупреждения hello в hello **по умолчанию YARN** группы установлено слишком**критическое**.</span><span class="sxs-lookup"><span data-stu-id="21c8d-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![диалоговое окно создания оповещения](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="21c8d-158">И, наконец, при выборе __Управление параметрами предупреждение__ из hello __действия__ меню позволяет tooset hello количество раз, предупреждение должно произойти, прежде чем будет отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="21c8d-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="21c8d-159">Этот параметр можно использовать tooprevent уведомления для временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="21c8d-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="21c8d-160">HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c8d-160">Cluster</span></span>

<span data-ttu-id="21c8d-161">Hello **метрики** hello панели мониторинга содержит ряд мини-приложения, благодаря которым она легко toomonitor hello состояния кластера с одного взгляда.</span><span class="sxs-lookup"><span data-stu-id="21c8d-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="21c8d-162">Если щелкнуть некоторые мини-приложения, например **Загрузка ЦП**, отобразится дополнительная информация.</span><span class="sxs-lookup"><span data-stu-id="21c8d-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![панель мониторинга с метриками](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="21c8d-164">Hello **Heatmaps** вкладку отображает показатели в виде цветной heatmaps, начиная от зеленого toored.</span><span class="sxs-lookup"><span data-stu-id="21c8d-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![панель мониторинга с тепловыми картами](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="21c8d-166">Дополнительные сведения о hello узлами в кластере hello выберите **узлов**.</span><span class="sxs-lookup"><span data-stu-id="21c8d-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="21c8d-167">Затем выберите hello определенного узла, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="21c8d-167">Then select hello specific node you are interested in.</span></span>

![информация об узле](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="21c8d-169">Службы</span><span class="sxs-lookup"><span data-stu-id="21c8d-169">Services</span></span>

<span data-ttu-id="21c8d-170">Hello **служб** боковой панели на панель мониторинга hello обеспечивает быстрый анализ состояния hello hello служб, работающих в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="21c8d-171">Различные значки, используемые tooindicate состояния или действия, которые следует выполнить.</span><span class="sxs-lookup"><span data-stu-id="21c8d-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="21c8d-172">Например если служба toobe перезапуску отображается желтый повторный запуск символ.</span><span class="sxs-lookup"><span data-stu-id="21c8d-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![боковая панель «Службы»](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="21c8d-174">Hello службы, которые отображаются различаются типы кластеров HDInsight и версии.</span><span class="sxs-lookup"><span data-stu-id="21c8d-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="21c8d-175">Здесь отображаются службы Hello может отличаться от службы hello, которые отображаются для кластера.</span><span class="sxs-lookup"><span data-stu-id="21c8d-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="21c8d-176">При выборе службы отображаются более подробные сведения о службе hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-176">Selecting a service displays more detailed information on hello service.</span></span>

![сводные данные о службе](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="21c8d-178">Быстрые ссылки</span><span class="sxs-lookup"><span data-stu-id="21c8d-178">Quick links</span></span>

<span data-ttu-id="21c8d-179">Некоторые службы отображения **быстрые ссылки** ссылку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="21c8d-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="21c8d-180">Это может быть web конкретной службы используется tooaccess пользовательских интерфейсов, таких как:</span><span class="sxs-lookup"><span data-stu-id="21c8d-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="21c8d-181">**Журнал заданий** — журнал заданий MapReduce;</span><span class="sxs-lookup"><span data-stu-id="21c8d-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="21c8d-182">**Диспетчер ресурсов** — пользовательский интерфейс диспетчера ресурсов YARN;</span><span class="sxs-lookup"><span data-stu-id="21c8d-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="21c8d-183">**NameNode** — пользовательский интерфейс NameNode распределенной файловой системы Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="21c8d-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="21c8d-184">**Веб-интерфейс Oozie** — пользовательский интерфейс Oozie.</span><span class="sxs-lookup"><span data-stu-id="21c8d-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="21c8d-185">Выбор любого из этих ссылок открывает новую вкладку в браузере, который отображает выбранную страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="21c8d-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="21c8d-186">Выбор hello **быстрые ссылки** входа для службы могут возвращать ошибку «сервер не найден».</span><span class="sxs-lookup"><span data-stu-id="21c8d-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="21c8d-187">Если эта ошибка возникает, необходимо использовать туннель SSH, при использовании hello **быстрые ссылки** входа для этой службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="21c8d-188">Дополнительные сведения см. в статье [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="21c8d-189">управления</span><span class="sxs-lookup"><span data-stu-id="21c8d-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="21c8d-190">Пользователи, группы и разрешения Ambari</span><span class="sxs-lookup"><span data-stu-id="21c8d-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="21c8d-191">Работа с пользователями, группами и разрешениями поддерживается только в [присоединенных к домену](hdinsight-domain-joined-introduction.md) кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c8d-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="21c8d-192">Сведения об использовании hello пользовательского интерфейса управления Ambari в кластере, присоединенных к домену см. в разделе [управление кластерами HDInsight на присоединенных к домену](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="21c8d-193">Не изменяйте пароль hello контрольного Ambari hello (hdinsightwatchdog) в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="21c8d-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="21c8d-194">Изменение разрывов пароль hello hello действия скрипта toouse возможности или выполнять операции масштабирования с кластером.</span><span class="sxs-lookup"><span data-stu-id="21c8d-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="21c8d-195">Узлы</span><span class="sxs-lookup"><span data-stu-id="21c8d-195">Hosts</span></span>

<span data-ttu-id="21c8d-196">Hello **узлов** странице перечислены все узлы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="21c8d-197">toomanage узлов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="21c8d-197">toomanage hosts, follow these steps.</span></span>

![страница «Узлы»](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="21c8d-199">В кластерах HDInsight не следует использовать добавление, списание и восстановление списанного узла.</span><span class="sxs-lookup"><span data-stu-id="21c8d-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="21c8d-200">Выберите узел hello, что вы хотите toomanage.</span><span class="sxs-lookup"><span data-stu-id="21c8d-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="21c8d-201">Используйте hello **действия** действие hello tooselect меню, что вы хотите tooperform:</span><span class="sxs-lookup"><span data-stu-id="21c8d-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="21c8d-202">**Запустить все компоненты** -запустить все компоненты на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="21c8d-203">**Остановить все компоненты** -остановить все компоненты на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="21c8d-204">**Перезапустите все компоненты** - остановка и запуск всех компонентов на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="21c8d-205">**Включить режим обслуживания** -подавляет предупреждения для узла hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="21c8d-206">Этот режим должен быть включен при выполнении действий, которые создают оповещения.</span><span class="sxs-lookup"><span data-stu-id="21c8d-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="21c8d-207">Например, остановка и запуск службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="21c8d-208">**Выключить режим обслуживания** -возвращает hello предупреждения toonormal узла.</span><span class="sxs-lookup"><span data-stu-id="21c8d-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="21c8d-209">**Остановить** -DataNode останавливается или NodeManagers на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="21c8d-210">**Запуск** -запускает DataNode или NodeManagers на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="21c8d-211">**Перезапустите** -останавливается и начинается DataNode или NodeManagers на узле hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="21c8d-212">**Списание** -Удаляет узел из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="21c8d-213">Не используйте это действие в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c8d-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="21c8d-214">**Recommission** -добавляет кластер ранее списанные toohello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="21c8d-215">Не используйте это действие в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c8d-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="21c8d-216"><a id="service"></a>Службы</span><span class="sxs-lookup"><span data-stu-id="21c8d-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="21c8d-217">Из hello **мониторинга** или **службы** используйте hello **действия** кнопку внизу hello hello список toostop службы и запускать все службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Действия со службой](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="21c8d-219">Хотя **добавить службу** указан в этом меню не должно возникать кластера HDInsight toohello используется tooadd службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="21c8d-220">Для добавления новых служб следует использовать действие сценария во время подготовки кластера.</span><span class="sxs-lookup"><span data-stu-id="21c8d-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="21c8d-221">Дополнительные сведения об использовании действий скрипта см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="21c8d-222">При hello **действия** кнопку можно перезапустить все службы, часто необходимо toostart, остановки и перезапуска службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="21c8d-223">Используйте следующие шаги действий tooperform на отдельной службы hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="21c8d-224">Из hello **мониторинга** или **служб** выберите службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="21c8d-225">Сверху "hello" hello **Сводка** используйте hello **действий службы** кнопки и выберите hello tootake действие.</span><span class="sxs-lookup"><span data-stu-id="21c8d-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="21c8d-226">Это перезапуск службы hello на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="21c8d-226">This restarts hello service on all nodes.</span></span>

    ![действие в службе](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="21c8d-228">Перезапуск некоторых служб, во время работы hello могут формироваться предупреждения.</span><span class="sxs-lookup"><span data-stu-id="21c8d-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="21c8d-229">tooavoid предупреждений, можно использовать hello **действий службы** tooenable кнопку **режима обслуживания** для службы hello перед выполнением перезапуска hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="21c8d-230">После выбора действие hello **# op** входа вверху hello tooshow приращениями странице hello, возникающей выполняется фоновая операция.</span><span class="sxs-lookup"><span data-stu-id="21c8d-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="21c8d-231">Если настроен toodisplay, отображается список hello фоновые операции.</span><span class="sxs-lookup"><span data-stu-id="21c8d-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="21c8d-232">Если вы включили **режима обслуживания** для службы hello помните toodisable его с помощью hello **действий службы** кнопку после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="21c8d-233">tooconfigure службы, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="21c8d-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="21c8d-234">Из hello **мониторинга** или **служб** выберите службы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="21c8d-235">Выберите hello **Configs** отображается вкладку hello текущей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21c8d-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="21c8d-236">Отобразится также список предыдущих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="21c8d-236">A list of previous configurations is also displayed.</span></span>

    ![конфигурации](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="21c8d-238">Использовать конфигурацию hello toomodify поля, отображаемые hello, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="21c8d-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="21c8d-239">Или выберите предыдущую конфигурацию, а затем выберите **сделать текущим** tooroll резервное toohello предыдущие параметры.</span><span class="sxs-lookup"><span data-stu-id="21c8d-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="21c8d-240">Представления Ambari</span><span class="sxs-lookup"><span data-stu-id="21c8d-240">Ambari views</span></span>

<span data-ttu-id="21c8d-241">Ambari представления позволяют разработчикам tooplug элементы пользовательского интерфейса в hello Ambari веб-интерфейса с помощью hello [Framework представления Ambari](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="21c8d-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="21c8d-242">HDInsight предоставляет следующие представления с типами кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="21c8d-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="21c8d-243">Диспетчер очереди yarn: hello диспетчера очереди предоставляет простой пользовательский Интерфейс для просмотра и изменения YARN очереди.</span><span class="sxs-lookup"><span data-stu-id="21c8d-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="21c8d-244">Куст представление: hello Hive представление позволяет запросов Hive toorun непосредственно из веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="21c8d-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="21c8d-245">Можно сохранять запросы, просмотреть результаты, сохранения результатов toohello хранения данных кластера или загрузки результатов tooyour локальной системы.</span><span class="sxs-lookup"><span data-stu-id="21c8d-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="21c8d-246">Дополнительные сведения об использовании представлений Hive см. [здесь](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="21c8d-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="21c8d-247">Представление Tez: hello Tez представление позволяет toobetter понять и оптимизировать заданий.</span><span class="sxs-lookup"><span data-stu-id="21c8d-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="21c8d-248">Можно просмотреть сведения о том, как выполняются задания Tez и какие ресурсы используются.</span><span class="sxs-lookup"><span data-stu-id="21c8d-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
