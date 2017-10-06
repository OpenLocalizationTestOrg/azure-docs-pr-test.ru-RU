---
title: "aaaDashboard монитор, масштабирование, Настройка и гибридные подключения в службах BizTalk | Документы Microsoft"
description: "Дополнительные сведения об элементах управления hello и наблюдения за производительностью hello классического портала вкладок для службы BizTalk: панель мониторинга, монитор, масштабирование, Настройка и гибридных подключений. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="4a526-104">Просмотрите hello вкладки панели мониторинга, монитор, масштабирование, Настройка и гибридного подключения</span><span class="sxs-lookup"><span data-stu-id="4a526-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="4a526-105">После создания службы BizTalk и развертывания приложения, можно изменить некоторые параметры службы BizTalk hello и наблюдения за производительностью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="4a526-106">При открытии hello классический портал Azure, вы автоматически оказываетесь на hello **все ЭЛЕМЕНТЫ** tooview вкладку службы BizTalk, выделите службу BizTalk в hello **все ЭЛЕМЕНТЫ** tab или выберите hello **Службы BIZTALK** ; и затем выберите имя службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="4a526-107">Откроется новое окно с hello следующие вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="4a526-108">В данном разделе описываются эти вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="4a526-109">Быстрый запуск (</span><span class="sxs-lookup"><span data-stu-id="4a526-109">Quickstart (</span></span>![Быстрый запуск][Quickstart]<span data-ttu-id="4a526-111">)</span><span class="sxs-lookup"><span data-stu-id="4a526-111">)</span></span>
<span data-ttu-id="4a526-112">В зависимости от hello выпуск службы BizTalk все параметры в списке не могут быть доступны.</span><span class="sxs-lookup"><span data-stu-id="4a526-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="4a526-113"><strong>Получить средства hello</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="4a526-114">Загрузите hello пакета SDK служб BizTalk tooinstall hello шаблоны проектов Visual Studio на компьютере в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="4a526-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="4a526-115">Эти шаблоны создают hello <strong>службы BizTalk</strong> (мост) и hello <strong>артефактов службы BizTalk</strong> проектах Visual Studio (преобразования), которые являются tooyour развернутой службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="4a526-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Как я запустить с помощью hello Azure BizTalk Services SDK </a> и <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello Установка пакета SDK служб BizTalk Azure</a> списки hello tooget шагов работы.</span><span class="sxs-lookup"><span data-stu-id="4a526-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="4a526-117"><strong>Создание партнерских соглашений</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="4a526-118">Здравствуйте, открывается портал служб Azure BizTalk, размещенной в Azure, где добавлять партнеров и создавать X12 AS2 и соглашения EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="4a526-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="4a526-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> списки hello tooget шагов работы.</span><span class="sxs-lookup"><span data-stu-id="4a526-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="4a526-120"><strong>Дополнительные сведения о службах BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="4a526-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">центр обучения</a> toolearn Дополнительные сведения о службах BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="4a526-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="4a526-122">На панели задач hello внизу hello вы можете:</span><span class="sxs-lookup"><span data-stu-id="4a526-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="4a526-123"><strong>Управление</strong> развертыванием приложений</span><span class="sxs-lookup"><span data-stu-id="4a526-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="4a526-124">Откроется портал служб Azure BizTalk hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="4a526-125">Конфигурация tooEDI входа hello, включая добавление партнеров и создания X12 AS2, является Hello портале служб BizTalk и соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="4a526-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="4a526-126">Это является hello таким же, как <strong>создать партнера соглашения</strong> на hello <strong>быстрый запуск</strong> вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="4a526-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> содержатся дополнительные сведения о портале служб BizTalk hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="4a526-128"><strong>Сведения о соединении</strong> из пространства имен Access Control hello</span><span class="sxs-lookup"><span data-stu-id="4a526-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="4a526-129">При выборе сведения о соединении, затем hello пространства имен Access Control, поставщика по умолчанию, и ключ по умолчанию отображаются.</span><span class="sxs-lookup"><span data-stu-id="4a526-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="4a526-130">Вы можете скопировать эти значения.</span><span class="sxs-lookup"><span data-stu-id="4a526-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="4a526-131">Можно также открыть hello портал управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4a526-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="4a526-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Создание элемента управления доступом пространство имен</a> предоставляет дополнительные сведения о hello портал управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4a526-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="4a526-133"><strong>Синхронизировать ключи</strong> в hello учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="4a526-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="4a526-134">При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="4a526-135">Эти ключи шифрования управления tooyour доступа к учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a526-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="4a526-136">Службы BizTalk автоматически использует hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="4a526-137"><strong>Синхронизировать ключи</strong> включить tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="4a526-138">Например вы хотите hello службы BizTalk toouse новый первичный ключ для hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a526-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="4a526-139">toodo это:</span><span class="sxs-lookup"><span data-stu-id="4a526-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="4a526-140">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="4a526-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="4a526-141">Выберите hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-141">Select hello Secondary Key.</span></span> <span data-ttu-id="4a526-142">При этом служба BizTalk hello запускается с помощью hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="4a526-143">В hello классический портал Azure выберите учетную запись хранилища и повторно создать первичный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="4a526-144">Помните, что служба BizTalk использует hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="4a526-145">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="4a526-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="4a526-146">Теперь щелкните hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="4a526-147">Это является hello new при повторном создании первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="4a526-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="4a526-148">В hello классический портал Azure выберите учетную запись хранилища и повторно создать вторичный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="4a526-149">Этот процесс называется «переключение ключей».</span><span class="sxs-lookup"><span data-stu-id="4a526-149">This process is called "rollover keys".</span></span> <span data-ttu-id="4a526-150">Назначение Hello — tooenable tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="4a526-151"><strong>Удаление</strong> приложения</span><span class="sxs-lookup"><span data-stu-id="4a526-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="4a526-152">При выборе удалить службу BizTalk, а все элементы, которые развернуты tooit удаляются.</span><span class="sxs-lookup"><span data-stu-id="4a526-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="4a526-153">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="4a526-153">Dashboard</span></span>
<span data-ttu-id="4a526-154">В зависимости от hello выпуск службы BizTalk все параметры в списке не могут быть доступны.</span><span class="sxs-lookup"><span data-stu-id="4a526-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="4a526-155">При выборе имя службы BizTalk, отображается вкладка сводки hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="4a526-156">На панели мониторинга можно выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4a526-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="4a526-157">Общие сведения об использовании: Показывает hello количество используемых гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="4a526-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="4a526-158">Также отображает hello использование данных в ГБ.</span><span class="sxs-lookup"><span data-stu-id="4a526-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="4a526-159">Диаграмма метрик. Отображается фиксированный список метрик производительности</span><span class="sxs-lookup"><span data-stu-id="4a526-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="4a526-160">Эти показатели предоставляют значения в реальном времени работоспособности hello hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="4a526-161">Вы также можете hello **относительный** или **абсолютный** значения и hello временной диапазон **интервал** hello метрик, отображаемых на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="4a526-162">Описание этих метрик производительности, go слишком[доступные метрики](#Metrics) в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="4a526-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="4a526-163">Краткий обзор. Перечисление свойств службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="4a526-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="4a526-164"><strong>Обновление учетных данных базы данных отслеживания</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="4a526-165">Здравствуйте, изменения имени пользователя и пароль, используемые toolog в hello базы данных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="4a526-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-166"><strong>Обновление SSL-сертификата</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="4a526-167">Можно обновить hello службы BizTalk toouse другой сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="4a526-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="4a526-168">Самозаверяющий SSL-сертификат автоматически создается при вы <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">создать службу BizTalk hello</a>.</span><span class="sxs-lookup"><span data-stu-id="4a526-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-169"><strong>Скачивание сертификата</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="4a526-170">Вы можете загрузить hello SSL-сертификаты, используемые на локальный компьютер tooa службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-171"><strong>Состояние</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="4a526-172">Отображает текущее состояние hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="4a526-173">См. раздел <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Службы BizTalk: диаграмма состояния службы</a>.</span><span class="sxs-lookup"><span data-stu-id="4a526-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="4a526-174"><strong>URL-адрес службы</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="4a526-175">Hello URL-адрес службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="4a526-176">Это же является hello как hello <strong>URL-адрес домена</strong> вводятся при создании службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-177"><strong>Общедоступный виртуальный IP-адрес (VIP-адрес)</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="4a526-178">tooyour IP-адреса, назначенного Hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="4a526-179">Он используется для всех входных конечных точек и hello исходный адрес для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="4a526-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="4a526-180">Этот IP-адрес принадлежит tooyour службы BizTalk, при условии, что она создана.</span><span class="sxs-lookup"><span data-stu-id="4a526-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="4a526-181">При удалении службы BizTalk hello hello IP-адрес назначается tooanother службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-182"><strong>Пространство имен ACS</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="4a526-183">Выполняет проверку подлинности с hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-184"><strong>Выпуск</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="4a526-185">Список hello введенный выпуска при создании службы BizTalk hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-186"><strong>Расположение</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="4a526-187">Отображает hello географического региона, в которой размещена ваша служба BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-188"><strong>Создано</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="4a526-189">Hello отображает дату и время hello была создана служба BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-190"><strong>База данных отслеживания</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="4a526-191">Имя базы данных SQL Azure Hello, которое хранит hello отслеживания таблиц, используемых службой BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="4a526-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Требования к Explained</a> предоставляет подробные сведения о hello базы данных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="4a526-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-193"><strong>Хранилище для мониторинга и архивации</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="4a526-194">Hello имя учетной записи хранилища Azure, сохраняет hello, отслеживающую выходные данные службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="4a526-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Требования к Explained</a> предоставляет подробные сведения о hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a526-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-196"><strong>Имя подписки</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="4a526-197">Список hello подписки, в которой размещена ваша служба BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="4a526-198">Hello подписка регулирует доступ toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4a526-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-199"><strong>Идентификатор подписки</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="4a526-200">Идентификатор подписки создается автоматически во время создания подписки.</span><span class="sxs-lookup"><span data-stu-id="4a526-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="4a526-201">При использовании интерфейсов API REST, может потребоваться tooenter hello, идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="4a526-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="4a526-202">[Службы BizTalk: Подготовка классический портал Azure с помощью](http://go.microsoft.com/fwlink/p/?LinkID=302280) списки hello toocreate действия службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="4a526-203">Управление, сведения о соединении, синхронизация ключей и удаления на панели задач hello:</span><span class="sxs-lookup"><span data-stu-id="4a526-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="4a526-204"><strong>Управление</strong> развертыванием приложений</span><span class="sxs-lookup"><span data-stu-id="4a526-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="4a526-205">Здравствуйте, открывается портал служб Azure BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="4a526-206">Конфигурация tooEDI входа hello, включая добавление партнеров и создания X12 AS2, является Hello портале служб BizTalk и соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="4a526-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="4a526-207">Это является hello таким же, как <strong>создать партнера соглашения</strong> на hello <strong>быстрый запуск</strong> вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="4a526-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> содержатся дополнительные сведения о портале служб BizTalk hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-209"><strong>Сведения о соединении</strong> из пространства имен Access Control hello</span><span class="sxs-lookup"><span data-stu-id="4a526-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="4a526-210">Отображает hello пространства имен Access Control, поставщика по умолчанию и ключ по умолчанию значения; которого могут быть скопированы.</span><span class="sxs-lookup"><span data-stu-id="4a526-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="4a526-211">Можно также открыть hello портал управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4a526-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="4a526-212">Этот портал управления доступом является hello такой же, как с помощью параметра Active Directory hello hello левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="4a526-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="4a526-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Управление Your пространство имен ACS</a> содержатся дополнительные сведения о hello портал управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4a526-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-214"><strong>Синхронизировать ключи</strong> в hello учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="4a526-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="4a526-215">При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="4a526-216">Эти ключи шифрования управления tooyour доступа к учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a526-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="4a526-217">Службы BizTalk автоматически использует hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="4a526-218"><strong>Синхронизировать ключи</strong> включить tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="4a526-219">Например вы хотите hello службы BizTalk toouse новый первичный ключ для hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a526-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="4a526-220">toodo это:</span><span class="sxs-lookup"><span data-stu-id="4a526-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="4a526-221">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="4a526-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="4a526-222">Выберите hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-222">Select hello Secondary Key.</span></span> <span data-ttu-id="4a526-223">При этом служба BizTalk hello запускается с помощью hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="4a526-224">В hello классический портал Azure выберите учетную запись хранилища и повторно создать первичный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="4a526-225">Помните, что служба BizTalk использует hello вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="4a526-226">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="4a526-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="4a526-227">Теперь щелкните hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="4a526-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="4a526-228">Это является hello new при повторном создании первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="4a526-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="4a526-229">В hello классический портал Azure выберите учетную запись хранилища и повторно создать вторичный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="4a526-230">Этот процесс называется «переключение ключей».</span><span class="sxs-lookup"><span data-stu-id="4a526-230">This process is called "rollover keys".</span></span> <span data-ttu-id="4a526-231">Назначение Hello — tooenable tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="4a526-232"><strong>Удаление</strong> приложения</span><span class="sxs-lookup"><span data-stu-id="4a526-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="4a526-233">Службы BizTalk и tooit все элементы развертывания, удаляются.</span><span class="sxs-lookup"><span data-stu-id="4a526-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="4a526-234">Монитор</span><span class="sxs-lookup"><span data-stu-id="4a526-234">Monitor</span></span>
<span data-ttu-id="4a526-235">Не применяется toohello бесплатный выпуск.</span><span class="sxs-lookup"><span data-stu-id="4a526-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="4a526-236">При выборе имя службы BizTalk hello монитор вкладка доступна и отображает hello следующие:</span><span class="sxs-lookup"><span data-stu-id="4a526-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="4a526-237">График метрики: Hello отображает выбранные метрики производительности</span><span class="sxs-lookup"><span data-stu-id="4a526-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="4a526-238">Эти показатели предоставляют значения в реальном времени работоспособности hello hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="4a526-239">Выбор метрик производительности осуществляется пользователем.</span><span class="sxs-lookup"><span data-stu-id="4a526-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="4a526-240">Одновременно может отображаться до шести метрик производительности.</span><span class="sxs-lookup"><span data-stu-id="4a526-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="4a526-241">Вы также можете hello **относительный** или **абсолютный** значения и hello временной диапазон **интервал** hello метрик, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="4a526-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="4a526-242">метрики tooremove или для отображения на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="4a526-243">Выберите hello **монитор** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="4a526-244">Выберите **добавить метрики** на панели задач hello:</span><span class="sxs-lookup"><span data-stu-id="4a526-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="4a526-245">![Выберите «Добавить метрику»][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="4a526-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="4a526-246">Проверьте метрики производительности hello требуется toodisplay.</span><span class="sxs-lookup"><span data-stu-id="4a526-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="4a526-247">Выберите hello флажок tooreturn toohello **монитор** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a526-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="4a526-248">Выберите hello круг Далее toohello метрики toodisplay значение этого показателя в hello graph.</span><span class="sxs-lookup"><span data-stu-id="4a526-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="4a526-249">Например, hello **ЦП** серым метрика; его выходные данные не отображаются в hello graph:</span><span class="sxs-lookup"><span data-stu-id="4a526-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="4a526-250">![Метрика загрузки ЦП неактивна][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="4a526-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="4a526-251">Выберите hello серым hello круг tooenable **ЦП** метрики toodisplay выходные данные в диаграмме hello:</span><span class="sxs-lookup"><span data-stu-id="4a526-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="4a526-252">![Метрика загрузки ЦП активна][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="4a526-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="4a526-253">Выберите метрику из диаграммы отображения hello и список hello tooremove **удалить метрику** на панели задач hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="4a526-254">tooadd hello метрики задней toohello выберите **добавить метрики** в панели задач hello, проверьте метрики hello и toohello tooreturn флажком выберите hello **монитор** вкладки. Выберите hello серым метрика hello tooenable круга.</span><span class="sxs-lookup"><span data-stu-id="4a526-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="4a526-255"><a name="Metrics"></a>Доступные метрики</span><span class="sxs-lookup"><span data-stu-id="4a526-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="4a526-256">доступны следующие счетчики производительности и показатели Hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="4a526-257"><strong>Задержка кругового пути</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="4a526-258">Отображает hello среднее время в миллисекундах (мс) tooprocess сообщение от приветственное сообщение hello время получения, пока сообщение hello полностью обрабатывается hello службы BizTalk через все мосты.</span><span class="sxs-lookup"><span data-stu-id="4a526-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="4a526-259">Учитываются только успешно обработанные сообщения.</span><span class="sxs-lookup"><span data-stu-id="4a526-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="4a526-260">Когда происходят следующие события hello, создается отметку времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="4a526-261">Поступления сообщения hello шлюза</span><span class="sxs-lookup"><span data-stu-id="4a526-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="4a526-262">Сообщение является перенаправленное toohello назначения</span><span class="sxs-lookup"><span data-stu-id="4a526-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="4a526-263">Получение ответа из места назначения</span><span class="sxs-lookup"><span data-stu-id="4a526-263">Destination response is received</span></span></li>
<li><span data-ttu-id="4a526-264">Отправлено ответов toohello назначения подтверждения шлюза</span><span class="sxs-lookup"><span data-stu-id="4a526-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="4a526-265">Эта Метрика показывает результат hello hello следующие вычисления:</span><span class="sxs-lookup"><span data-stu-id="4a526-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="4a526-266">[Адрес подтверждение отправлено ответов toohello шлюз] - [поступления сообщения hello шлюза]</span><span class="sxs-lookup"><span data-stu-id="4a526-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-267"><strong>Сбои в источнике</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="4a526-268">Отображает общее количество сообщений, которые не удалось hello, hello службы BizTalk, когда удаление сообщений из конечных точек источника hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-269"><strong>Загрузка ЦП</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="4a526-270">Список hello среднее время процессора для всех экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="4a526-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-271"><strong>Задержка обработки</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="4a526-272">Отображает среднее время hello в миллисекундах (мс) tooprocess сообщение по hello службы BizTalk через все мосты, за исключением hello времени, затраченное на назначения.</span><span class="sxs-lookup"><span data-stu-id="4a526-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="4a526-273">Учитываются только успешно обработанные сообщения.</span><span class="sxs-lookup"><span data-stu-id="4a526-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="4a526-274">Если каждый hello следующие события происходят, создается отметку времени:</span><span class="sxs-lookup"><span data-stu-id="4a526-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="4a526-275">Поступления сообщения hello шлюза</span><span class="sxs-lookup"><span data-stu-id="4a526-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="4a526-276">Сообщение является перенаправленное toohello назначения</span><span class="sxs-lookup"><span data-stu-id="4a526-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="4a526-277">Получение ответа из места назначения</span><span class="sxs-lookup"><span data-stu-id="4a526-277">Destination response is received</span></span></li>
<li><span data-ttu-id="4a526-278">Отправлено ответов toohello назначения подтверждения шлюза</span><span class="sxs-lookup"><span data-stu-id="4a526-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="4a526-279">Эта Метрика показывает результат hello hello следующие вычисления:</span><span class="sxs-lookup"><span data-stu-id="4a526-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="4a526-280">[Адрес подтверждение отправлено ответов toohello шлюз] - [шлюза hello поступления сообщения] - [назначения ответ] + [сообщение является назначение перенаправленное toohello]</span><span class="sxs-lookup"><span data-stu-id="4a526-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-281"><strong>Сбои при обработке</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="4a526-282">Отображает hello общее количество сообщений, сбой во время обработки, hello службы BizTalk через все мосты hello в течение интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-283"><strong>Отправленные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="4a526-284">Отображает hello общее количество сообщений, отправленных hello службы BizTalk через все мосты в течение интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="4a526-285">Эта метрика увеличивается, когда сообщение, отправленное из конвейера достигает hello назначение маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="4a526-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="4a526-286">Данная метрика не указывает, что сообщение успешно обработано.</span><span class="sxs-lookup"><span data-stu-id="4a526-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="4a526-287">В сценарии "запрос-ответ" метрика hello увеличивается, когда назначение маршрутизации hello отправляет конвейера toohello назад подтверждение поступления.</span><span class="sxs-lookup"><span data-stu-id="4a526-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-288"><strong>Полученные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="4a526-289">Отображает hello общее количество сообщений, полученных hello службы BizTalk через все мосты в течение интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="4a526-290">Эта метрика увеличивается при получении нового сообщения hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="4a526-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-291"><strong>Сообщения в обработке</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="4a526-292">Отображает hello общее количество сообщений, которые в настоящее время обрабатываемые hello службы BizTalk в течение интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="4a526-293"><strong>Обработанные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="4a526-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="4a526-294">Отображает hello общее количество сообщений, успешно обрабатываемых hello службы BizTalk через все мосты в течение интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4a526-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="4a526-295">Эта метрика увеличивается, если сообщение получено конвейера hello и успешно перенаправленное toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="4a526-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="4a526-296">Масштаб</span><span class="sxs-lookup"><span data-stu-id="4a526-296">Scale</span></span>
<span data-ttu-id="4a526-297">Во вкладке "масштаб" hello можно добавить или вычесть hello число единиц, используемых службой BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="4a526-298">По умолчанию настроен один модуль.</span><span class="sxs-lookup"><span data-stu-id="4a526-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="4a526-299">Дополнительные единицы можно добавить tooscale службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="4a526-300">При увеличении масштаба hello увеличивая пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="4a526-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="4a526-301">также увеличивается Hello объем ресурсов, включая развернутых мостов, соглашения, связей бизнес-ОБЪЕКТОВ и вычислительной мощности.</span><span class="sxs-lookup"><span data-stu-id="4a526-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="4a526-302">Например вы увеличиваете hello шкала от 1 too2 модульные единицы.</span><span class="sxs-lookup"><span data-stu-id="4a526-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="4a526-303">В этом случае можно развернуть число double hello мосты, double hello соглашений, double hello LOB соединения и двойные hello вычислительной мощности.</span><span class="sxs-lookup"><span data-stu-id="4a526-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="4a526-304">Некоторые выпуски BizTalk не поддерживают параметр масштаба.</span><span class="sxs-lookup"><span data-stu-id="4a526-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="4a526-305">В этом случае разрешен только один модуль.</span><span class="sxs-lookup"><span data-stu-id="4a526-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="4a526-306">toodetermine количество единиц, можно масштабировать выпуска, см. слишком[службы BizTalk: схема с выпусками](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="4a526-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="4a526-307">Увеличение числа hello единиц может повлиять на цены.</span><span class="sxs-lookup"><span data-stu-id="4a526-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="4a526-308">При увеличении hello единицы выборе **Сохранить** отображает сообщение, информирующее о том, если это повлияет на выставление счетов.</span><span class="sxs-lookup"><span data-stu-id="4a526-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="4a526-309">Затем необходимо выбрать toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4a526-309">You then choose toocontinue.</span></span> <span data-ttu-id="4a526-310">При увеличении hello число единиц, изменяет Active tooUpdating hello состояние службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="4a526-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="4a526-311">В hello обновление состояния службы BizTalk продолжает toorun.</span><span class="sxs-lookup"><span data-stu-id="4a526-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="4a526-312">[Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md) определяет «единицу измерения».</span><span class="sxs-lookup"><span data-stu-id="4a526-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="4a526-313">Настройка</span><span class="sxs-lookup"><span data-stu-id="4a526-313">Configure</span></span>
<span data-ttu-id="4a526-314">Не применяется tooHybrid подключений.</span><span class="sxs-lookup"><span data-stu-id="4a526-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="4a526-315">Задает состояние архивации tooNone hello или автоматически.</span><span class="sxs-lookup"><span data-stu-id="4a526-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="4a526-316">Если значение tooNone, резервные копии не создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="4a526-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="4a526-317">Если значение tooAutomatic, настройте расположение резервной копии hello, частота hello hello резервного копирования, и как долго tookeep hello резервного копирования файлов.</span><span class="sxs-lookup"><span data-stu-id="4a526-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="4a526-318">[Службы BizTalk: Резервное копирование и восстановление](biztalk-backup-restore.md) подробно описаны hello.</span><span class="sxs-lookup"><span data-stu-id="4a526-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="4a526-319"><a name="HybridConnections"></a>Гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="4a526-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="4a526-320">Гибридные подключения подключают приложения Azure, такие как веб-приложения и мобильные приложения в службе приложений Azure, tooan локального ресурса, который использует статический TCP-порт, например SQL Server, MySQL, HTTP веб-API и наиболее пользовательских веб-служб.</span><span class="sxs-lookup"><span data-stu-id="4a526-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="4a526-321">Гибридные подключения осуществляется в службах BizTalk в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4a526-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="4a526-322">в разделе toocreate гибридных подключений в службе приложений Azure, [доступа к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a526-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="4a526-323">toocreate или управлять гибридных подключений в службах BizTalk Azure см. в разделе [гибридные подключения](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a526-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="4a526-324">Далее</span><span class="sxs-lookup"><span data-stu-id="4a526-324">Next</span></span>
<span data-ttu-id="4a526-325">Теперь, когда вы знакомы с разных вкладках hello, можно узнать больше о возможностях службы Azure BizTalk hello:</span><span class="sxs-lookup"><span data-stu-id="4a526-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="4a526-326">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="4a526-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="4a526-327">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="4a526-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="4a526-328">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="4a526-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="4a526-329">См. также</span><span class="sxs-lookup"><span data-stu-id="4a526-329">See Also</span></span>
* [<span data-ttu-id="4a526-330">Гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="4a526-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="4a526-331">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="4a526-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="4a526-332">Создание служб BizTalk с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4a526-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="4a526-333">Службы BizTalk: диаграмма состояния службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="4a526-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="4a526-334">Как я запустить с помощью hello пакета SDK служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="4a526-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

