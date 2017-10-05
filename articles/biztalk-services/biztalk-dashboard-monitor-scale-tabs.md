---
title: "Панель мониторинга, мониторинг, масштаб, настройка и гибридные подключения в службах BizTalk | Документация Майкрософт"
description: "Дополнительная информация об элементах управления и наблюдении за производительностью на вкладках классического портала для служб BizTalk: панель мониторинга, монитор, масштаб, настройка и гибридные подключения. MABS, WABS"
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
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="139b0-104">Просмотр вкладок «Панель мониторинга», «Монитор», «Масштаб», «Настройка» и «Гибридное подключение»</span><span class="sxs-lookup"><span data-stu-id="139b0-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="139b0-105">После создания службы BizTalk и развертывания приложения можно изменить некоторые параметры службы BizTalk и отслеживать производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="139b0-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="139b0-106">При запуске классического портала Azure автоматически открывается вкладка **ВСЕ ЭЛЕМЕНТЫ** .</span><span class="sxs-lookup"><span data-stu-id="139b0-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="139b0-107">Чтобы просмотреть службу BizTalk, выберите ее на вкладке **Все элементы** или откройте вкладку **Службы BIZTALK**, а затем выберите имя нужной службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="139b0-108">Будет открыто новое окно со следующими вкладками.</span><span class="sxs-lookup"><span data-stu-id="139b0-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="139b0-109">В данном разделе описываются эти вкладки.</span><span class="sxs-lookup"><span data-stu-id="139b0-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="139b0-110">Быстрый запуск (</span><span class="sxs-lookup"><span data-stu-id="139b0-110">Quickstart (</span></span>![Быстрый запуск][Quickstart]<span data-ttu-id="139b0-112">)</span><span class="sxs-lookup"><span data-stu-id="139b0-112">)</span></span>
<span data-ttu-id="139b0-113">В зависимости от версии служб BizTalk не все параметры в списке могут быть доступны.</span><span class="sxs-lookup"><span data-stu-id="139b0-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="139b0-114"><strong>Получение инструментов</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="139b0-115">Загрузите пакет SDK служб BizTalk для установки шаблонов проектов Visual Studio на локальном компьютере, предназначенном для разработки.</span><span class="sxs-lookup"><span data-stu-id="139b0-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="139b0-116">Эти шаблоны создают проекты Visual Studio для <strong>служб BizTalk</strong> (мост) и <strong>артефактов служб BizTalk</strong> (преобразование), которые развертываются в службе BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="139b0-117">В разделах 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> Использование пакета SDK для служб BizTalk в Azure</a> и <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Установка пакета SDK служб BizTalk Azure</a> содержатся инструкции по началу работы.</span><span class="sxs-lookup"><span data-stu-id="139b0-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="139b0-118"><strong>Создание партнерских соглашений</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="139b0-119">Открывает портал служб BizTalk в Azure (размещенный в Azure), где выполняется добавление партнеров, а также создание соглашений X12, AS2 и EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="139b0-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="139b0-120">Шаги по началу работы описаны в разделе 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка EDI, AS2 и EDIFACT на портале служб BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="139b0-121"><strong>Дополнительные сведения о службах BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="139b0-122">Дополнительные сведения о службах BizTalk в Azure см. в <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">центре обучения</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="139b0-123">На панели задач внизу можно воспользоваться следующими функциями.</span><span class="sxs-lookup"><span data-stu-id="139b0-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="139b0-124"><strong>Управление</strong> развертыванием приложений</span><span class="sxs-lookup"><span data-stu-id="139b0-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="139b0-125">Открывает портал служб BizTalk в Azure.</span><span class="sxs-lookup"><span data-stu-id="139b0-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="139b0-126">Портал служб BizTalk является точкой входа в конфигурацию EDI, в том числе для добавления партнеров и создания соглашений X12, AS2 и EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="139b0-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="139b0-127">Это аналог команды <strong>Создать партнерские соглашения</strong> на вкладке <strong>Быстрый запуск</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="139b0-128">Дополнительные сведения о портале служб BizTalk см. в разделе о 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">настройке компонентов для обмена сообщениями EDI на портале служб BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="139b0-129"><strong>Сведения о подключении</strong> пространства имен управления доступом</span><span class="sxs-lookup"><span data-stu-id="139b0-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="139b0-130">При выборе команды "Сведения о подключении" отображаются параметры "Пространство имен управления доступом", "Издатель по умолчанию" и "Ключ по умолчанию".</span><span class="sxs-lookup"><span data-stu-id="139b0-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="139b0-131">Вы можете скопировать эти значения.</span><span class="sxs-lookup"><span data-stu-id="139b0-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="139b0-132">Вы также можете открыть портал контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="139b0-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="139b0-133">Дополнительную информацию о портале контроля доступа см. в статье <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Инструкции по созданию пространства имен Access Control</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="139b0-134"><strong>Синхронизация ключей</strong> в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="139b0-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="139b0-135">При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="139b0-136">Эти ключи шифрования позволяют управлять доступом к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="139b0-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="139b0-137">Служба BizTalk автоматически использует первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="139b0-138">Команда <strong>Синхронизировать ключи</strong> позволяет пользователям переключаться между первичным и вторичным ключами, не прерывая работу службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="139b0-139">Например, пусть вам требуется, чтобы служба BizTalk использовала новый первичный ключ для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="139b0-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="139b0-140">Для этого:</span><span class="sxs-lookup"><span data-stu-id="139b0-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="139b0-141">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="139b0-142">Выберите вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-142">Select the Secondary Key.</span></span> <span data-ttu-id="139b0-143">После этого в службе BizTalk будет использоваться этот вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="139b0-144">На классическом портале Azure выберите свою учетную запись хранения и заново создайте первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="139b0-145">Помните, что в службе BizTalk используется вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="139b0-146">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="139b0-147">Теперь выберите первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-147">Now, select the Primary Key.</span></span> <span data-ttu-id="139b0-148">Это новый первичный ключ, который был создан повторно.</span><span class="sxs-lookup"><span data-stu-id="139b0-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="139b0-149">На классическом портале Azure выберите свою учетную запись хранения и заново создайте вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="139b0-150">Этот процесс называется «переключение ключей».</span><span class="sxs-lookup"><span data-stu-id="139b0-150">This process is called "rollover keys".</span></span> <span data-ttu-id="139b0-151">Его цель — позволить пользователям переключаться между первичным и вторичным ключами без прерывания работы службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="139b0-152"><strong>Удаление</strong> приложения</span><span class="sxs-lookup"><span data-stu-id="139b0-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="139b0-153">При нажатии кнопки "Удалить" служба BizTalk будет удалена вместе со всеми развернутыми в ней элементами.</span><span class="sxs-lookup"><span data-stu-id="139b0-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="139b0-154">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="139b0-154">Dashboard</span></span>
<span data-ttu-id="139b0-155">В зависимости от версии служб BizTalk не все параметры в списке могут быть доступны.</span><span class="sxs-lookup"><span data-stu-id="139b0-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="139b0-156">Если вы выберете имя своей службы BizTalk, появится вкладка "Панель мониторинга".</span><span class="sxs-lookup"><span data-stu-id="139b0-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="139b0-157">На панели мониторинга можно выполнять следующие действия.</span><span class="sxs-lookup"><span data-stu-id="139b0-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="139b0-158">Обзор использования. Отображение количества используемых гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="139b0-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="139b0-159">Также отображает использование данных в GB.</span><span class="sxs-lookup"><span data-stu-id="139b0-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="139b0-160">Диаграмма метрик. Отображается фиксированный список метрик производительности</span><span class="sxs-lookup"><span data-stu-id="139b0-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="139b0-161">Эти метрики содержат обновляемые в реальном времени значения, отражающие работоспособность службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="139b0-162">Также можно выбрать **относительные** или **абсолютные** значения и **интервал** диапазона времени для метрик, отображаемых в графике.</span><span class="sxs-lookup"><span data-stu-id="139b0-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="139b0-163">Описание этих метрик производительности см. в этой статье в разделе [Доступные метрики](#Metrics).</span><span class="sxs-lookup"><span data-stu-id="139b0-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="139b0-164">Краткий обзор. Перечисление свойств службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="139b0-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="139b0-165"><strong>Обновление учетных данных базы данных отслеживания</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="139b0-166">Изменение имени пользователя и пароля, которые используются для входа в базу данных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="139b0-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-167"><strong>Обновление SSL-сертификата</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="139b0-168">Может изменить службу BizTalk так, чтобы в ней использовался другой SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="139b0-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="139b0-169">При <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">создании службы BizTalk</a> автоматически создается самозаверяющий сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="139b0-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-170"><strong>Скачивание сертификата</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="139b0-171">SSL-сертификат, который используется службой BizTalk, можно загрузить на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="139b0-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-172"><strong>Состояние</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="139b0-173">Отображение текущего состояния службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="139b0-174">См. раздел <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Службы BizTalk: диаграмма состояния службы</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="139b0-175"><strong>URL-адрес службы</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="139b0-176">URL-адрес службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="139b0-177">Совпадает с параметром <strong>URL-адрес домена</strong>, который вводится при создании службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-178"><strong>Общедоступный виртуальный IP-адрес (VIP-адрес)</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="139b0-179">IP-адрес, присвоенный службе BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="139b0-180">Он используется для всех конечных точек ввода и является адресом источника для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="139b0-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="139b0-181">Указанный IP-адрес принадлежит данной службе BizTalk во время ее создания.</span><span class="sxs-lookup"><span data-stu-id="139b0-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="139b0-182">При удалении службы BizTalk данный IP-адрес присваивается другой службе BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-183"><strong>Пространство имен ACS</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="139b0-184">Проверка подлинности с помощью службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-185"><strong>Выпуск</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="139b0-186">Выводит список выпуска при создании службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-187"><strong>Расположение</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="139b0-188">Отображает географический регион, в котором размещается служба BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-189"><strong>Создано</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="139b0-190">Показывает дату и время создания службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-191"><strong>База данных отслеживания</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="139b0-192">Имя базы данных SQL Azure, в которой хранятся таблицы отслеживания, используемые в службе BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="139b0-193">В разделе 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Пояснение требований</a> представлены сведения о базе данных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="139b0-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-194"><strong>Хранилище для мониторинга и архивации</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="139b0-195">Имя учетной записи хранения Azure, в которой хранятся выходные данные мониторинга службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="139b0-196">В разделе 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Пояснение требований</a> представлены сведения о об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="139b0-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-197"><strong>Имя подписки</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="139b0-198">Выводит список подписки, на котором размещена служба BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="139b0-199">Эта подписка обеспечивает доступ к классическому порталу Azure.</span><span class="sxs-lookup"><span data-stu-id="139b0-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-200"><strong>Идентификатор подписки</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="139b0-201">Идентификатор подписки создается автоматически во время создания подписки.</span><span class="sxs-lookup"><span data-stu-id="139b0-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="139b0-202">Если вы используете API REST, вам может понадобиться ввести этот идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="139b0-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="139b0-203">[Создание служб BizTalk с помощью портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) .</span><span class="sxs-lookup"><span data-stu-id="139b0-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="139b0-204">Управление, сведения о подключении, синхронизация ключей и удаление на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="139b0-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="139b0-205"><strong>Управление</strong> развертыванием приложений</span><span class="sxs-lookup"><span data-stu-id="139b0-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="139b0-206">Открывает портал служб BizTalk в Azure.</span><span class="sxs-lookup"><span data-stu-id="139b0-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="139b0-207">Портал служб BizTalk является точкой входа в конфигурацию EDI, в том числе для добавления партнеров и создания соглашений X12, AS2 и EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="139b0-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="139b0-208">Это аналог команды <strong>Создать партнерские соглашения</strong> на вкладке <strong>Быстрый запуск</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="139b0-209">Дополнительные сведения о портале служб BizTalk см. в разделе о 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">настройке компонентов для обмена сообщениями EDI на портале служб BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-210"><strong>Сведения о подключении</strong> пространства имен управления доступом</span><span class="sxs-lookup"><span data-stu-id="139b0-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="139b0-211">Отображает пространство имен Access Control, значения "Издатель по умолчанию" и "Ключ по умолчанию", которые можно скопировать.</span><span class="sxs-lookup"><span data-stu-id="139b0-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="139b0-212">Вы также можете открыть портал контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="139b0-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="139b0-213">Работа с этим порталом аналогична использованию параметра Active Directory в области навигации слева.</span><span class="sxs-lookup"><span data-stu-id="139b0-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="139b0-214">Дополнительные сведения о портале контроля доступа см. в статье об 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">управлении пространством имен ACS</a>.</span><span class="sxs-lookup"><span data-stu-id="139b0-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-215"><strong>Синхронизация ключей</strong> в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="139b0-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="139b0-216">При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="139b0-217">Эти ключи шифрования позволяют управлять доступом к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="139b0-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="139b0-218">Служба BizTalk автоматически использует первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="139b0-219">Команда <strong>Синхронизировать ключи</strong> позволяет пользователям переключаться между первичным и вторичным ключами, не прерывая работу службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="139b0-220">Например, пусть вам требуется, чтобы служба BizTalk использовала новый первичный ключ для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="139b0-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="139b0-221">Для этого:</span><span class="sxs-lookup"><span data-stu-id="139b0-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="139b0-222">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="139b0-223">Выберите вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-223">Select the Secondary Key.</span></span> <span data-ttu-id="139b0-224">После этого в службе BizTalk будет использоваться этот вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="139b0-225">На классическом портале Azure выберите свою учетную запись хранения и заново создайте первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="139b0-226">Помните, что в службе BizTalk используется вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="139b0-227">Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>.</span><span class="sxs-lookup"><span data-stu-id="139b0-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="139b0-228">Теперь выберите первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-228">Now, select the Primary Key.</span></span> <span data-ttu-id="139b0-229">Это новый первичный ключ, который был создан повторно.</span><span class="sxs-lookup"><span data-stu-id="139b0-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="139b0-230">На классическом портале Azure выберите свою учетную запись хранения и заново создайте вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="139b0-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="139b0-231">Этот процесс называется «переключение ключей».</span><span class="sxs-lookup"><span data-stu-id="139b0-231">This process is called "rollover keys".</span></span> <span data-ttu-id="139b0-232">Его цель — позволить пользователям переключаться между первичным и вторичным ключами без прерывания работы службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="139b0-233"><strong>Удаление</strong> приложения</span><span class="sxs-lookup"><span data-stu-id="139b0-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="139b0-234">Служба BizTalk и все элементы, развернутые для нее, удаляются.</span><span class="sxs-lookup"><span data-stu-id="139b0-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="139b0-235">Монитор</span><span class="sxs-lookup"><span data-stu-id="139b0-235">Monitor</span></span>
<span data-ttu-id="139b0-236">Неприменимо к выпуску Free Edition.</span><span class="sxs-lookup"><span data-stu-id="139b0-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="139b0-237">При выборе имени службы BizTalk Service доступна вкладка "Монитор", на которой отображаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="139b0-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="139b0-238">Диаграмма метрик. Отображаются выбранные метрики производительности</span><span class="sxs-lookup"><span data-stu-id="139b0-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="139b0-239">Эти метрики содержат обновляемые в реальном времени значения, отражающие работоспособность службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="139b0-240">Выбор метрик производительности осуществляется пользователем.</span><span class="sxs-lookup"><span data-stu-id="139b0-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="139b0-241">Одновременно может отображаться до шести метрик производительности.</span><span class="sxs-lookup"><span data-stu-id="139b0-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="139b0-242">Также можно выбрать **относительные** или **абсолютные** значения и **интервал** диапазона времени для метрик, отображаемых на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="139b0-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="139b0-243">Отображение метрик на диаграмме и их удаление.</span><span class="sxs-lookup"><span data-stu-id="139b0-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="139b0-244">Выберите вкладку **Монитор** .</span><span class="sxs-lookup"><span data-stu-id="139b0-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="139b0-245">Выберите **Добавить метрики** на панели задач:</span><span class="sxs-lookup"><span data-stu-id="139b0-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="139b0-246">![Выберите «Добавить метрику»][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="139b0-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="139b0-247">Проверьте метрики производительности, которые должны отображаться.</span><span class="sxs-lookup"><span data-stu-id="139b0-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="139b0-248">Щелкните по флажку, чтобы вернуться на вкладку **Монитор** .</span><span class="sxs-lookup"><span data-stu-id="139b0-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="139b0-249">Чтобы вывести значение метрики на диаграмме, щелкните кружок рядом с этой метрикой.</span><span class="sxs-lookup"><span data-stu-id="139b0-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="139b0-250">Например, метрика **Загрузка ЦП** затенена (неактивна), и ее выходные данные не отображаются на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="139b0-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="139b0-251">![Метрика загрузки ЦП неактивна][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="139b0-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="139b0-252">Чтобы активировать метрику **Загрузка ЦП** и отобразить ее выходные данные на диаграмме, щелкните затененный кружок.</span><span class="sxs-lookup"><span data-stu-id="139b0-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="139b0-253">![Метрика загрузки ЦП активна][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="139b0-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="139b0-254">Чтобы удалить метрику из диаграммы и списка, выберите **Удалить метрики** на панели задач.</span><span class="sxs-lookup"><span data-stu-id="139b0-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="139b0-255">Чтобы вернуть метрику в список, выберите **Добавить метрики** на панели задач, отметьте нужную метрику и установите флажок, чтобы вернуться на вкладку **Монитор**.</span><span class="sxs-lookup"><span data-stu-id="139b0-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="139b0-256">Выберите затененный кружок, чтобы включить метрику.</span><span class="sxs-lookup"><span data-stu-id="139b0-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="139b0-257"><a name="Metrics"></a>Доступные метрики</span><span class="sxs-lookup"><span data-stu-id="139b0-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="139b0-258">Доступны следующие счетчики производительности и метрики.</span><span class="sxs-lookup"><span data-stu-id="139b0-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="139b0-259"><strong>Задержка кругового пути</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="139b0-260">Отображает среднее значение времени в миллисекундах (мс), необходимое для обработки сообщений с момента получения до момента завершения обработки службой BizTalk во всех мостах.</span><span class="sxs-lookup"><span data-stu-id="139b0-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="139b0-261">Учитываются только успешно обработанные сообщения.</span><span class="sxs-lookup"><span data-stu-id="139b0-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="139b0-262">При наступлении следующих событий создается отметка времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="139b0-263">Поступление сообщения в шлюз</span><span class="sxs-lookup"><span data-stu-id="139b0-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="139b0-264">Направление сообщения в место назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="139b0-265">Получение ответа из места назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-265">Destination response is received</span></span></li>
<li><span data-ttu-id="139b0-266">Отправка в шлюз подтверждения из места назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="139b0-267">Метрика показывает результат следующего расчета:</span><span class="sxs-lookup"><span data-stu-id="139b0-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="139b0-268">[Отправка в шлюз подтверждения из места назначения] — [Поступление сообщения в шлюз]</span><span class="sxs-lookup"><span data-stu-id="139b0-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-269"><strong>Сбои в источнике</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="139b0-270">Отображает общее число сообщений, не принятых службой BizTalk при извлечении сообщений из конечных точек источника.</span><span class="sxs-lookup"><span data-stu-id="139b0-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-271"><strong>Загрузка ЦП</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="139b0-272">Показывает средний процент загруженности процессора для всех экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="139b0-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-273"><strong>Задержка обработки</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="139b0-274">Отображает среднее время в миллисекундах (мс), затрачиваемое на обработку сообщения службой BizTalk во всех мостах (в миллисекундах), без учета времени, затрачиваемого в местах назначения.</span><span class="sxs-lookup"><span data-stu-id="139b0-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="139b0-275">Учитываются только успешно обработанные сообщения.</span><span class="sxs-lookup"><span data-stu-id="139b0-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="139b0-276">При наступлении каждого следующих событий создается отметка времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="139b0-277">Поступление сообщения в шлюз</span><span class="sxs-lookup"><span data-stu-id="139b0-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="139b0-278">Направление сообщения в место назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="139b0-279">Получение ответа из места назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-279">Destination response is received</span></span></li>
<li><span data-ttu-id="139b0-280">Отправка в шлюз подтверждения из места назначения</span><span class="sxs-lookup"><span data-stu-id="139b0-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="139b0-281">Метрика показывает результат следующего расчета:</span><span class="sxs-lookup"><span data-stu-id="139b0-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="139b0-282">[Отправка в шлюз подтверждения из места назначения] — [Поступление сообщения в шлюз] — [Получение ответа из места назначения] + [Направление сообщения в место назначения]</span><span class="sxs-lookup"><span data-stu-id="139b0-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-283"><strong>Сбои при обработке</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="139b0-284">Указывает общее количество сообщений со сбоем в ходе обработки службой BizTalk во всех мостах за определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-285"><strong>Отправленные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="139b0-286">Указывает общее количество сообщений, отправленных службой BizTalk во всех мостах за определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="139b0-287">Эта метрика увеличивается, когда отправленное из конвейера сообщение достигает места назначения.</span><span class="sxs-lookup"><span data-stu-id="139b0-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="139b0-288">Данная метрика не указывает, что сообщение успешно обработано.</span><span class="sxs-lookup"><span data-stu-id="139b0-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="139b0-289">В сценарии запроса и ответа эта метрика увеличивается, когда из места назначения в конвейер оправляется подтверждение получения.</span><span class="sxs-lookup"><span data-stu-id="139b0-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-290"><strong>Полученные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="139b0-291">Указывает общее количество сообщений, полученных службой BizTalk во всех мостах за определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="139b0-292">Эта метрика увеличивается при поступлении нового сообщения на конвейер.</span><span class="sxs-lookup"><span data-stu-id="139b0-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-293"><strong>Сообщения в обработке</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="139b0-294">Указывает общее количество сообщений, в настоящее время находящихся в обработке службой BizTalk, за определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="139b0-295"><strong>Обработанные сообщения</strong></span><span class="sxs-lookup"><span data-stu-id="139b0-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="139b0-296">Указывает общее количество сообщений, успешно обработанных службой BizTalk во всех мостах за определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="139b0-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="139b0-297">Эта метрика увеличивается в том случае, если сообщение успешно получено конвейером и передано по назначению.</span><span class="sxs-lookup"><span data-stu-id="139b0-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="139b0-298">Масштаб</span><span class="sxs-lookup"><span data-stu-id="139b0-298">Scale</span></span>
<span data-ttu-id="139b0-299">На вкладке «Масштаб» можно добавлять и уменьшать число модулей, используемых службой BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="139b0-300">По умолчанию настроен один модуль.</span><span class="sxs-lookup"><span data-stu-id="139b0-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="139b0-301">Можно добавить дополнительные модули для масштабирования службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="139b0-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="139b0-302">При увеличении масштаба растет пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="139b0-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="139b0-303">Также увеличивается объем ресурсов, включая разворачиваемые мосты, соглашения, бизнес-подключения и вычислительные мощности.</span><span class="sxs-lookup"><span data-stu-id="139b0-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="139b0-304">Например, пусть масштаб увеличивается с 1 модуля до 2 модулей.</span><span class="sxs-lookup"><span data-stu-id="139b0-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="139b0-305">В этом случае можно развернуть двойное число мостов, в два раза больше соглашений, вдвое увеличить число бизнес-подключений и вычислительную мощность.</span><span class="sxs-lookup"><span data-stu-id="139b0-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="139b0-306">Некоторые выпуски BizTalk не поддерживают параметр масштаба.</span><span class="sxs-lookup"><span data-stu-id="139b0-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="139b0-307">В этом случае разрешен только один модуль.</span><span class="sxs-lookup"><span data-stu-id="139b0-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="139b0-308">Для определения числа единиц, до которого можно масштабировать выпуск, см. статью [Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="139b0-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="139b0-309">Увеличение числа модулей может повлиять на цену.</span><span class="sxs-lookup"><span data-stu-id="139b0-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="139b0-310">Если выбрать команду **Сохранить** после увеличения количества модулей, выводится сообщение, указывающее, будет ли это отражено при выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="139b0-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="139b0-311">Затем можно продолжить сохранение.</span><span class="sxs-lookup"><span data-stu-id="139b0-311">You then choose to continue.</span></span> <span data-ttu-id="139b0-312">При увеличении числа модулей состояние службы BizTalk изменится с "Активно" на "Обновление".</span><span class="sxs-lookup"><span data-stu-id="139b0-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="139b0-313">В состоянии "Обновление" служба BizTalk продолжает работать.</span><span class="sxs-lookup"><span data-stu-id="139b0-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="139b0-314">[Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md) определяет «единицу измерения».</span><span class="sxs-lookup"><span data-stu-id="139b0-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="139b0-315">Настройка</span><span class="sxs-lookup"><span data-stu-id="139b0-315">Configure</span></span>
<span data-ttu-id="139b0-316">Неприменимо для гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="139b0-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="139b0-317">Устанавливает состояние резервного копирования в значение "Нет" или "Автоматически".</span><span class="sxs-lookup"><span data-stu-id="139b0-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="139b0-318">При установке в значение "Нет" не происходит автоматического создания резервных копий.</span><span class="sxs-lookup"><span data-stu-id="139b0-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="139b0-319">При значении "Автоматически" вы выполняете настройку местоположения резервной копии, частоты резервного копирования и срока хранения файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="139b0-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="139b0-320">[Службы BizTalk: резервное копирование и восстановление](biztalk-backup-restore.md) предоставляет подробную информацию.</span><span class="sxs-lookup"><span data-stu-id="139b0-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="139b0-321"><a name="HybridConnections"></a>Гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="139b0-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="139b0-322">Гибридные подключения связывают приложения Azure (например, веб-приложения или мобильные приложения в службе приложений Azure), с локальным ресурсом, который использует статический порт TCP (например, SQL Server, MySQL, веб-API для HTTP и большинство настраиваемых веб-служб).</span><span class="sxs-lookup"><span data-stu-id="139b0-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="139b0-323">Управление гибридными подключениями в службах BizTalk осуществляется на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="139b0-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="139b0-324">Сведения о создании гибридных подключений в службе приложений Azure см. в статье [Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="139b0-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="139b0-325">Сведения о создании гибридных подключений и управлении ими в службах Azure BizTalk см. в разделе [Гибридные подключения](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="139b0-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="139b0-326">Далее</span><span class="sxs-lookup"><span data-stu-id="139b0-326">Next</span></span>
<span data-ttu-id="139b0-327">Теперь, когда вы ознакомились с различными вкладками, вы можете получить дополнительные сведения о возможностях служб BizTalk в Azure.</span><span class="sxs-lookup"><span data-stu-id="139b0-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="139b0-328">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="139b0-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="139b0-329">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="139b0-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="139b0-330">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="139b0-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="139b0-331">См. также</span><span class="sxs-lookup"><span data-stu-id="139b0-331">See Also</span></span>
* [<span data-ttu-id="139b0-332">Гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="139b0-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="139b0-333">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="139b0-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="139b0-334">Создание служб BizTalk с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="139b0-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="139b0-335">Службы BizTalk: диаграмма состояния службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="139b0-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="139b0-336">Как приступить к работе с пакетом SDK для служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="139b0-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

