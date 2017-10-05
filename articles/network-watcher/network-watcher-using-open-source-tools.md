---
title: "Визуализация распределения сетевого трафика с помощью Наблюдателя за сетями Azure и средств с открытым кодом | Документация Майкрософт"
description: "На этой странице описывается, как использовать захват пакетов Наблюдателя за сетями со средством CapAnalysis для визуализации распределения входящего и исходящего трафика на виртуальных машинах."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="c535b-103">Визуализация распределения входящего и исходящего трафика на виртуальных машинах с помощью средств с открытым кодом</span><span class="sxs-lookup"><span data-stu-id="c535b-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="c535b-104">Захват пакетов содержит сетевые данные, которые позволяют выполнять экспертизу сети и тщательную проверку пакетов.</span><span class="sxs-lookup"><span data-stu-id="c535b-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="c535b-105">Есть множество средств с открытым кодом, которые можно использовать для анализа захвата пакетов, чтобы получить ценную информацию о сети.</span><span class="sxs-lookup"><span data-stu-id="c535b-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="c535b-106">В числе таких средств можно назвать средство с открытым кодом CapAnalysis, предназначенное для визуализации захвата пакетов.</span><span class="sxs-lookup"><span data-stu-id="c535b-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="c535b-107">Визуализация данных захвата пакетов позволяет быстро получать информацию о тенденциях и аномалиях в сети.</span><span class="sxs-lookup"><span data-stu-id="c535b-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="c535b-108">Также визуализация позволяет передавать такую информацию другим людям в простом и доступном формате.</span><span class="sxs-lookup"><span data-stu-id="c535b-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="c535b-109">Наблюдатель за сетями Azure позволяет собирать эти ценные данные, предоставляя функцию захвата пакетов в сети.</span><span class="sxs-lookup"><span data-stu-id="c535b-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="c535b-110">Эта статья содержит пошаговое руководство по визуализации и анализу данных захвата пакетов с помощью CapAnalysis и Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="c535b-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c535b-111">Сценарий</span><span class="sxs-lookup"><span data-stu-id="c535b-111">Scenario</span></span>

<span data-ttu-id="c535b-112">На виртуальной машине Azure развернуто простое веб-приложение, для которого вы хотите выполнить визуализацию сетевого трафика с помощью средств с открытым кодом, чтобы быстро понять распределение потоков и возможные аномалии.</span><span class="sxs-lookup"><span data-stu-id="c535b-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="c535b-113">Наблюдатель за сетями позволяет получить захват пакетов конкретной сетевой среды и сохранить эти данные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c535b-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="c535b-114">После этого CapAnalysis может принять захват пакетов непосредственно из BLOB-объекта хранилища и визуализировать его содержимое.</span><span class="sxs-lookup"><span data-stu-id="c535b-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![сценарий][1]

## <a name="steps"></a><span data-ttu-id="c535b-116">Действия</span><span class="sxs-lookup"><span data-stu-id="c535b-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="c535b-117">Установка CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="c535b-117">Install CapAnalysis</span></span>

<span data-ttu-id="c535b-118">Чтобы установить CapAnalysis на виртуальной машине, воспользуйтесь официальной инструкцией, доступной по адресу https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="c535b-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="c535b-119">Для удаленного доступа к CapAnalysis необходимо открыть на виртуальной машине порт 9877. Для этого добавьте новое правило безопасности для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="c535b-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="c535b-120">Дополнительные сведения о создании правил в группах безопасности сети см. в разделе [Создание правил в существующей сетевой группе безопасности](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="c535b-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="c535b-121">Когда правило будет добавлено, вы сможете получить доступ к CapAnalysis из `http://<PublicIP>:9877`.</span><span class="sxs-lookup"><span data-stu-id="c535b-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="c535b-122">Запуск сеанса захвата пакетов в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="c535b-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="c535b-123">Наблюдатель за сетями позволяет захватить все пакеты для отслеживания входящего и исходящего трафика на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c535b-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="c535b-124">Инструкции о том, как начать сеанс захвата пакетов, есть в статье [Manage packet captures with Azure Network Watcher using the portal](network-watcher-packet-capture-manage-portal.md) (Управление захватом пакетов с помощью Наблюдателя за сетями на портале).</span><span class="sxs-lookup"><span data-stu-id="c535b-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="c535b-125">Полученный захват пакетов можно сохранить в хранилище BLOB-объектов, к которому затем получит доступ CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="c535b-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="c535b-126">Передача захвата пакетов в CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="c535b-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="c535b-127">Вы можете напрямую отправить захват пакетов, полученный Наблюдателем за сетями, на вкладке "Импортировать с URL-адреса", где нужно указать ссылку на BLOB-объект хранилища, в котором хранится захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="c535b-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="c535b-128">Передавая ссылку в CapAnalysis, не забудьте добавить маркер SAS к URL-адресу BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="c535b-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="c535b-129">Чтобы создать этот маркер, откройте в учетной записи хранения подписанный URL-адрес, назначьте необходимые разрешения и нажмите кнопку "Создать SAS".</span><span class="sxs-lookup"><span data-stu-id="c535b-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="c535b-130">Полученный маркер SAS затем можно добавить к URL-адресу захвата пакетов в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="c535b-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="c535b-131">Полученный URL-адрес будет выглядеть примерно следующим образом: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="c535b-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="c535b-132">Анализ захвата пакетов</span><span class="sxs-lookup"><span data-stu-id="c535b-132">Analyzing packet captures</span></span>

<span data-ttu-id="c535b-133">CapAnalysis предлагает много возможностей для визуализации захвата пакетов, позволяющих выполнить анализ с разных точек зрения.</span><span class="sxs-lookup"><span data-stu-id="c535b-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="c535b-134">Эти наглядные сводки помогают понять тенденции распределения сетевого трафика и быстро выявлять любые необычные действия.</span><span class="sxs-lookup"><span data-stu-id="c535b-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="c535b-135">В следующем списке показаны некоторые из этих возможностей.</span><span class="sxs-lookup"><span data-stu-id="c535b-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="c535b-136">Таблицы потоков</span><span class="sxs-lookup"><span data-stu-id="c535b-136">Flow Tables</span></span>

    <span data-ttu-id="c535b-137">Эта таблица содержит список потоков, содержащихся в данных о пакетах, с указанием меток времени и различных протоколов, связанных с каждым потоком, а также IP-адресов источника и получателя.</span><span class="sxs-lookup"><span data-stu-id="c535b-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![Страница потоков CapAnalysis][5]

1. <span data-ttu-id="c535b-139">Обзор протоколов</span><span class="sxs-lookup"><span data-stu-id="c535b-139">Protocol Overview</span></span>

    <span data-ttu-id="c535b-140">Эта панель позволяет быстро просматривать распределение сетевого трафика по разным протоколам и географическим регионам.</span><span class="sxs-lookup"><span data-stu-id="c535b-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![Обзор протоколов CapAnalysis][6]

1. <span data-ttu-id="c535b-142">Статистика</span><span class="sxs-lookup"><span data-stu-id="c535b-142">Statistics</span></span>

    <span data-ttu-id="c535b-143">Эта панель позволяет просматривать статистику сетевого трафика по таким параметрам, как количество отправленных и полученных байтов для IP-адресов источника и получателя, количество потоков для каждого IP-адреса источника и получателя, используемые в потоках протоколы и продолжительность потоков.</span><span class="sxs-lookup"><span data-stu-id="c535b-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![Статистика CapAnalysis][7]

1. <span data-ttu-id="c535b-145">Географическая карта</span><span class="sxs-lookup"><span data-stu-id="c535b-145">Geomap</span></span>

    <span data-ttu-id="c535b-146">Эта панель содержит представление карты сетевого трафика, на которой с помощью цветов закодирован объем трафика из каждой страны.</span><span class="sxs-lookup"><span data-stu-id="c535b-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="c535b-147">Вы можете выбрать отдельные страны для просмотра дополнительных данных о потоках. Например, здесь можно увидеть соотношение отправленных и полученных данных для IP-адресов определенной страны.</span><span class="sxs-lookup"><span data-stu-id="c535b-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![Географическая карта][8]

1. <span data-ttu-id="c535b-149">Фильтры</span><span class="sxs-lookup"><span data-stu-id="c535b-149">Filters</span></span>

    <span data-ttu-id="c535b-150">CapAnalysis предоставляет набор фильтров для быстрого анализа пакетов определенного типа.</span><span class="sxs-lookup"><span data-stu-id="c535b-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="c535b-151">Например, можно фильтровать данные по протоколу, чтобы подробнее изучить распределение этого подмножества трафика.</span><span class="sxs-lookup"><span data-stu-id="c535b-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="c535b-153">Дополнительные сведения о возможностях CapAnalysis см. на странице [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about).</span><span class="sxs-lookup"><span data-stu-id="c535b-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c535b-154">Заключение</span><span class="sxs-lookup"><span data-stu-id="c535b-154">Conclusion</span></span>

<span data-ttu-id="c535b-155">Функция захвата пакетов Наблюдателя за сетями позволяет сохранять полезные данные для экспертизы сети и понимания характеристик сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="c535b-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="c535b-156">На этом примере мы показали, как можно легко интегрировать захват пакетов Наблюдателя за сетями со средствами визуализации с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="c535b-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="c535b-157">Используя средства с открытым кодом для визуализации захвата пакетов, например CapAnalysis, вы можете тщательно проверять сетевые пакеты и быстро выявлять тенденции трафика в сети.</span><span class="sxs-lookup"><span data-stu-id="c535b-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c535b-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c535b-158">Next steps</span></span>

<span data-ttu-id="c535b-159">Информацию о журналах потоков для групп безопасности сети см. [в этой статье](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c535b-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="c535b-160">Ознакомьтесь со статьей [Visualizing Network Security Group flow logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Визуализация журналов потоков для групп безопасности сети с помощью Power BI).</span><span class="sxs-lookup"><span data-stu-id="c535b-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
