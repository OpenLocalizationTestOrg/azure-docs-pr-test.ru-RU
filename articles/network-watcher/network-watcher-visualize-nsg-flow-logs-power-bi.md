---
title: "Заносит в журнал aaaVisualizing сетевой группы безопасности Azure потока с Power BI | Документы Microsoft"
description: "Эта страница описывает, каким образом ведет журнал toovisualize NSG потока с помощью Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="a685b-103">Визуализация журналов потоков для групп безопасности сети с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="a685b-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="a685b-104">Сетевая группа безопасности потока журналы позволяют tooview сведения о входящего и исходящего трафика IP на группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a685b-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="a685b-105">Эти журналы потока Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о hello потока (источник и назначение IP-адресов, исходного или целевого порта протокола), и если hello трафик разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="a685b-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="a685b-106">Это может быть трудно toogain анализировать потока, ведение журнала данных путем поиска hello файлов журнала вручную.</span><span class="sxs-lookup"><span data-stu-id="a685b-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="a685b-107">В этой статье мы предоставляем toovisualize решение, к последней потока журналов и узнавать о трафика в сети.</span><span class="sxs-lookup"><span data-stu-id="a685b-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="a685b-108">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a685b-108">Scenario</span></span>

<span data-ttu-id="a685b-109">В следующие сценарии hello мы подключитесь учетную запись хранилища Power BI toohello рабочего стола, мы указали в качестве приемника hello наши данные NSG потока ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a685b-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="a685b-110">После подключения учетной записи хранилища tooour, Power BI загружает и выполняет синтаксический анализ tooprovide журналы hello визуальное представление hello трафика, который регистрирует группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a685b-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="a685b-111">С помощью визуальных элементов hello, указанное в шаблоне hello, в котором можно просмотреть:</span><span class="sxs-lookup"><span data-stu-id="a685b-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="a685b-112">наиболее активные источники трафика;</span><span class="sxs-lookup"><span data-stu-id="a685b-112">Top Talkers</span></span>
* <span data-ttu-id="a685b-113">данные потоков временных рядов по направлениям и типам правил;</span><span class="sxs-lookup"><span data-stu-id="a685b-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="a685b-114">потоки по MAC-адресам сетевых интерфейсов;</span><span class="sxs-lookup"><span data-stu-id="a685b-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="a685b-115">потоки по группам безопасности сети и правилам;</span><span class="sxs-lookup"><span data-stu-id="a685b-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="a685b-116">потоки по конечным портам.</span><span class="sxs-lookup"><span data-stu-id="a685b-116">Flows by Destination Port</span></span>

<span data-ttu-id="a685b-117">Hello шаблона, предоставленного для редактирования, можно изменить его tooadd новых данных с визуальными элементами, или изменить запросы toosuit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="a685b-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="a685b-118">Настройка</span><span class="sxs-lookup"><span data-stu-id="a685b-118">Setup</span></span>

<span data-ttu-id="a685b-119">Прежде чем мы начнем работу, вам необходимо включить журналы потоков для одной или нескольких групп безопасности сети в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a685b-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="a685b-120">Инструкции по включению сетевой безопасности потока журналов см. в следующей статьей toohello: [ведения журнала tooflow введение для групп безопасности сети](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a685b-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="a685b-121">Также необходимо иметь hello Power BI Desktop клиента установлено на компьютере и достаточно свободного пространства на компьютере toodownload и загрузка hello данные журнала, существующий в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="a685b-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Схема Visio][1]

### <a name="steps"></a><span data-ttu-id="a685b-123">Действия</span><span class="sxs-lookup"><span data-stu-id="a685b-123">Steps</span></span>

1. <span data-ttu-id="a685b-124">Загрузите и откройте hello после шаблона Power BI в Power BI Desktop приложения hello [потока PowerBI Наблюдатель сети входит шаблон](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="a685b-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="a685b-125">Введите параметры запроса требуется hello</span><span class="sxs-lookup"><span data-stu-id="a685b-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="a685b-126">**StorageAccountName** — toohello указывает имя учетной записи хранилища hello, содержащий поток NSG hello журналы, которые бы как tooload и визуализации.</span><span class="sxs-lookup"><span data-stu-id="a685b-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="a685b-127">**NumberOfLogFiles** — указывает количество файлов журнала, необходимо будет toodownload и визуализации в Power BI в hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="a685b-128">Например если указано 50 hello 50 последних файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="a685b-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="a685b-129">У нас есть 2 Nsg FF включена и настроена учетная запись toothis toosend NSG потока журналы, а затем hello последних 25 часов журналов можно просмотреть.</span><span class="sxs-lookup"><span data-stu-id="a685b-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![Главный экран Power BI][2]

1. <span data-ttu-id="a685b-131">Введите ключ доступа для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="a685b-132">Допустимые комбинации клавиш можно найти, перейдя по tooyour учетной записи хранилища в Azure, портала и щелкнув hello **клавиши доступа** из меню параметров hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="a685b-133">Щелкните **Подключить** и примените изменения.</span><span class="sxs-lookup"><span data-stu-id="a685b-133">Click **Connect** then apply changes.</span></span>

    ![ключи доступа][3]

    ![Ключи доступа (2)][4]

4.  <span data-ttu-id="a685b-136">Ваши журналы загрузить и проанализировать, и теперь можно использовать предварительно созданной hello визуальных элементов.</span><span class="sxs-lookup"><span data-stu-id="a685b-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="a685b-137">Основные сведения о визуальных элементах hello</span><span class="sxs-lookup"><span data-stu-id="a685b-137">Understanding hello visuals</span></span>

<span data-ttu-id="a685b-138">Хранение в hello не шаблона набор визуальных элементов, которые помогают смысла hello NSG журнала потока данных.</span><span class="sxs-lookup"><span data-stu-id="a685b-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="a685b-139">Hello следующих изображениях представлены образец hello панель мониторинга выглядит при заполняются данными.</span><span class="sxs-lookup"><span data-stu-id="a685b-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="a685b-140">Ниже мы подробнее рассмотрим каждый визуальный элемент.</span><span class="sxs-lookup"><span data-stu-id="a685b-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="a685b-142">Hello верхней Talkers visual показано hello IP-адресов, инициированная hello большинство подключений через указанный период hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="a685b-143">размер Hello hello поля соответствует toohello относительное количество подключений.</span><span class="sxs-lookup"><span data-stu-id="a685b-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![Наиболее активные источники трафика][6]

<span data-ttu-id="a685b-145">Hello следующие диаграммы для ряда времени Показать hello число потоков в течение периода hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="a685b-146">Hello верхнем графике, разбитых на направление потока hello и нижней hello, разбитых на hello, принятое ("Разрешить" или "Запретить").</span><span class="sxs-lookup"><span data-stu-id="a685b-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="a685b-147">Этот визуальный элемент позволяет изучить тенденции изменения трафика во времени, выявить необычные всплески активности, а также отклонения или сегментацию трафика.</span><span class="sxs-lookup"><span data-stu-id="a685b-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![Потоки по периодам][7]

<span data-ttu-id="a685b-149">Hello следующий график показывает потоки hello каждого сетевого интерфейса с верхней hello, разбитых на направление потока и hello ниже, разбитых на решение было принято.</span><span class="sxs-lookup"><span data-stu-id="a685b-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="a685b-150">С этой информацией, можно получить подробные сведения о которой виртуальные машины взаимодействуют hello большинство относительный tooothers и если трафик tooa определенную виртуальную Машину, разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="a685b-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![Потоки по сетевым интерфейсам][8]

<span data-ttu-id="a685b-152">Hello следующие колесо кольцевой график показывает распределение потоков, конечный порт.</span><span class="sxs-lookup"><span data-stu-id="a685b-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="a685b-153">Эти сведения можно просматривать hello наиболее часто используемые конечные порты, используемые в пределах указанного hello периода.</span><span class="sxs-lookup"><span data-stu-id="a685b-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![Кольцевая диаграмма][9]

<span data-ttu-id="a685b-155">Hello следующей диаграмме показан hello потока, NSG и правила.</span><span class="sxs-lookup"><span data-stu-id="a685b-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="a685b-156">С этой информацией вы увидите hello Nsg, отвечающий за hello большинство трафика и hello распределение трафика на NSG правилом.</span><span class="sxs-lookup"><span data-stu-id="a685b-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![Линейчатая диаграмма][10]
 
<span data-ttu-id="a685b-158">Hello следующие информационные диаграммы отображают информацию о Nsg hello присутствует в журналах hello, число потоков, собранных за период hello и Дата hello hello ранний журнал, захваченный hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="a685b-159">Таким образом можно понять, какие Nsg в журнале и hello диапазон дат потоков.</span><span class="sxs-lookup"><span data-stu-id="a685b-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![Информационная диаграмма 1][11]

![Информационная диаграмма 2][12]

<span data-ttu-id="a685b-162">Этот шаблон включает в себя hello следующие срезы tooallow вы tooview вас интересуют наиболее только данные hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="a685b-163">Вы можете использовать фильтры по группам ресурсов, группам безопасности сети и правилам.</span><span class="sxs-lookup"><span data-stu-id="a685b-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="a685b-164">Кроме того, можно также фильтровать по 5-фрагментному информации, принятия решений и hello время записи журнала hello.</span><span class="sxs-lookup"><span data-stu-id="a685b-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![Срезы][13]

## <a name="conclusion"></a><span data-ttu-id="a685b-166">Заключение</span><span class="sxs-lookup"><span data-stu-id="a685b-166">Conclusion</span></span>

<span data-ttu-id="a685b-167">Мы показали в этом сценарии, с помощью журналов потока группы безопасности сети, предоставляемых Наблюдатель сети и Power BI, мы могли toovisualize и понять hello трафика.</span><span class="sxs-lookup"><span data-stu-id="a685b-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="a685b-168">С помощью шаблона предоставленный hello, Power BI загружает журналы hello напрямую из хранилища и обрабатывает их локально.</span><span class="sxs-lookup"><span data-stu-id="a685b-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="a685b-169">Время, затраченное tooload hello шаблона зависит от hello количество файлов, запрошенных и общий размер файлов загружены.</span><span class="sxs-lookup"><span data-stu-id="a685b-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="a685b-170">При желании вы свободного toocustomize этот шаблон вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="a685b-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="a685b-171">Есть очень много способов применить Power BI в сочетании с журналами потоков для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a685b-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="a685b-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="a685b-172">Notes</span></span>

* <span data-ttu-id="a685b-173">Журналы по умолчанию хранятся в следующем расположении: `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="a685b-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="a685b-174">Если существуют другие данные в другом каталоге они hello toopull запросов и данных hello процесса необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="a685b-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="a685b-175">Hello указанный шаблон не рекомендуется для использования с более чем 1 ГБ журналов.</span><span class="sxs-lookup"><span data-stu-id="a685b-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="a685b-176">Если у вас очень много журналов для анализа, мы рекомендуем использовать другое хранилище данных, например Data Lake или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a685b-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a685b-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a685b-177">Next Steps</span></span>

<span data-ttu-id="a685b-178">Узнайте, как toovisualize вашего потока NSG заносит в журнал с hello Elastick стека, посетив [визуализировать tooand шаблоны сетевой трафик из виртуальных машин с помощью средств с открытым исходным кодом](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="a685b-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
