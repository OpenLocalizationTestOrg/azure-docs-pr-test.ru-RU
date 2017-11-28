---
title: "aaaVisualize сетевой трафик с Наблюдатель сети Azure и средств с открытым исходным кодом | Документы Microsoft"
description: "На этой странице описываются как пакет Наблюдатель сети toouse захвата с tooand Capanalysis toovisualize трафика шаблонов из виртуальных машин."
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
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="ac5b8-103">Визуализация tooand шаблоны сетевой трафик из виртуальных машин с помощью средств с открытым исходным кодом</span><span class="sxs-lookup"><span data-stu-id="ac5b8-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="ac5b8-104">Захват пакетов содержат данные сети, которые позволяют расследований tooperform сети и глубокую проверку пакетов.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="ac5b8-105">Существует много откроется средств источника, о сети можно использовать снимки toogain tooanalyze пакетов аналитики.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="ac5b8-106">В числе таких средств можно назвать средство с открытым кодом CapAnalysis, предназначенное для визуализации захвата пакетов.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="ac5b8-107">Визуализация данных отслеживания пакетов способ ценных tooquickly производные важные сведения о шаблонах и аномалий в сети.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="ac5b8-108">Также визуализация позволяет передавать такую информацию другим людям в простом и доступном формате.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="ac5b8-109">Наблюдатель сети Azure предоставляет hello toocapture возможности, которые записывает эти ценные данные, позволяя tooperform пакетов в сети.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="ac5b8-110">В этой статье мы предоставляем Пошаговое руководство по как захватывает Наблюдатель сети при помощи CapAnalysis toovisualize и приращение полезных сведений из пакета.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="ac5b8-111">Сценарий</span><span class="sxs-lookup"><span data-stu-id="ac5b8-111">Scenario</span></span>

<span data-ttu-id="ac5b8-112">У вас есть развертывания простого веб-приложения на виртуальной Машине в Azure требуется toouse открытой средства toovisualize его tooquickly трафика сети определить поток характер и любых возможных аномалий.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="ac5b8-113">Наблюдатель за сетями позволяет получить захват пакетов конкретной сетевой среды и сохранить эти данные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="ac5b8-114">CapAnalysis можно приема hello захват пакетов непосредственно из большого двоичного объекта хранилища hello и отобразить его содержимое.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![сценарий][1]

## <a name="steps"></a><span data-ttu-id="ac5b8-116">Действия</span><span class="sxs-lookup"><span data-stu-id="ac5b8-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="ac5b8-117">Установка CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="ac5b8-117">Install CapAnalysis</span></span>

<span data-ttu-id="ac5b8-118">tooinstall CapAnalysis на виртуальной машине, могут ссылаться инструкции официальный toohello https://www.capanalysis.net/ca/how-to-install-capanalysis здесь.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="ac5b8-119">В порядке удаленного доступа к CapAnalysis, то необходимо порт tooopen 9877 на ВМ путем добавления нового правила безопасности для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="ac5b8-120">Дополнительные сведения о создании правил в группах безопасности сети, см. слишком[создавать правила в существующей NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="ac5b8-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="ac5b8-121">После успешного добавления hello правило должно быть возможности tooaccess CapAnalysis из`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="ac5b8-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="ac5b8-122">Используйте пакет отслеживания сеанса toostart Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="ac5b8-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="ac5b8-123">Наблюдатель сети разрешает трафик tootrack toocapture пакетов и из него виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="ac5b8-124">Можно ссылаться инструкции toohello на [снимки управление пакетов с Наблюдатель сети](network-watcher-packet-capture-manage-portal.md) toostart сеанс отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="ac5b8-125">На этом снимке пакетов могут храниться в toobe хранилища больших двоичных объектов, доступ к CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="ac5b8-126">Отправка tooCapAnalysis захват пакетов</span><span class="sxs-lookup"><span data-stu-id="ac5b8-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="ac5b8-127">Захват пакетов, выполняемое Наблюдатель сети с помощью вкладки «Импорт из URL-адрес» hello и предоставляя toohello ссылку хранилища BLOB-объекта хранения hello захват пакетов можно передать напрямую.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="ac5b8-128">При предоставлении tooCapAnalysis ссылку, сделать tooappend убедиться, что URL-адрес SAS BLOB-объекта маркера toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="ac5b8-129">toodo, перейдите tooShared подписи доступа из учетной записи хранения hello, назначить hello разрешения и нажмите клавишу toocreate кнопку Создать SAS hello маркер.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="ac5b8-130">Затем можно добавить этот токен toohello пакетов записи хранилища больших двоичных объектов URL-адрес SAS.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="ac5b8-131">Hello полученный URL-адрес будет выглядеть примерно следующим образом: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="ac5b8-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="ac5b8-132">Анализ захвата пакетов</span><span class="sxs-lookup"><span data-stu-id="ac5b8-132">Analyzing packet captures</span></span>

<span data-ttu-id="ac5b8-133">CapAnalysis предлагает различные параметры toovisualize получения пакетов, каждый обеспечивает анализ из другой точки зрения.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="ac5b8-134">Эти наглядные сводки помогают понять тенденции распределения сетевого трафика и быстро выявлять любые необычные действия.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="ac5b8-135">Некоторые из этих компонентов, показаны в hello после списка.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="ac5b8-136">Таблицы потоков</span><span class="sxs-lookup"><span data-stu-id="ac5b8-136">Flow Tables</span></span>

    <span data-ttu-id="ac5b8-137">Это дает таблицы hello список потоках данных пакета hello, hello отметка времени, связанная с потоками hello и hello различных протоколов, связанных с потоком hello, а также исходный и конечный IP.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![Страница потоков CapAnalysis][5]

1. <span data-ttu-id="ac5b8-139">Обзор протоколов</span><span class="sxs-lookup"><span data-stu-id="ac5b8-139">Protocol Overview</span></span>

    <span data-ttu-id="ac5b8-140">Эта панель позволяет tooquickly просмотра hello распределение сетевого трафика за hello различные протоколы и географических регионах.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![Обзор протоколов CapAnalysis][6]

1. <span data-ttu-id="ac5b8-142">Статистика</span><span class="sxs-lookup"><span data-stu-id="ac5b8-142">Statistics</span></span>

    <span data-ttu-id="ac5b8-143">Эта панель позволяет вы tooview статистики по сетевому трафику — байт отправлено и получено из источника и назначения IP-адресов, потоков для каждого из hello исходный и конечный IP-адресов, использовать протокол для различных потоков, а также срок hello потоков.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![Статистика CapAnalysis][7]

1. <span data-ttu-id="ac5b8-145">Географическая карта</span><span class="sxs-lookup"><span data-stu-id="ac5b8-145">Geomap</span></span>

    <span data-ttu-id="ac5b8-146">Эта панель предоставляет представление карты сетевого трафика, с цветами, масштабирование toohello объем трафика из каждой страны.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="ac5b8-147">Вы можете выбрать выделенный стран tooview дополнительный поток статистику, например hello долю данных отправленных и полученных от IP-адресов в данной стране.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![Географическая карта][8]

1. <span data-ttu-id="ac5b8-149">Фильтры</span><span class="sxs-lookup"><span data-stu-id="ac5b8-149">Filters</span></span>

    <span data-ttu-id="ac5b8-150">CapAnalysis предоставляет набор фильтров для быстрого анализа пакетов определенного типа.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="ac5b8-151">Например вы можете toofilter hello данных с помощью протокола toogain конкретных аналитики на данном подмножестве трафика.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="ac5b8-153">Посетите [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn Дополнительные сведения о всех CapAnalysis возможности.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ac5b8-154">Заключение</span><span class="sxs-lookup"><span data-stu-id="ac5b8-154">Conclusion</span></span>

<span data-ttu-id="ac5b8-155">Функция записи пакетов Наблюдатель сети позволяет экспертизы toocapture hello данных необходимости tooperform сети и лучше понять сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="ac5b8-156">На этом примере мы показали, как можно легко интегрировать захват пакетов Наблюдателя за сетями со средствами визуализации с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="ac5b8-157">С помощью средств с открытым исходным кодом, таких как захватывает CapAnalysis toovisualize пакетов, можно выполнять тщательную проверку пакетов и быстро определить тенденции в пределах сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="ac5b8-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac5b8-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac5b8-158">Next steps</span></span>

<span data-ttu-id="ac5b8-159">Посетите toolearn Дополнительные сведения о журналах потока NSG, [журналы NSG потока](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ac5b8-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="ac5b8-160">Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="ac5b8-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
