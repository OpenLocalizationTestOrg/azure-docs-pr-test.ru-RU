---
title: "aaaTroubleshooting и мониторинга для SAP HANA в Azure (большие экземпляры) | Документы Microsoft"
description: "Сведения об устранении неполадок и мониторинге архитектуры решения \"SAP HANA в Azure (крупные экземпляры)\"."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="c6568-103">Как tootroubleshoot и мониторинга SAP HANA (крупных экземпляров) в Azure</span><span class="sxs-lookup"><span data-stu-id="c6568-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c6568-104">Мониторинг архитектуры SAP HANA в Azure (крупные экземпляры)</span><span class="sxs-lookup"><span data-stu-id="c6568-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c6568-105">SAP HANA в Azure (большие экземпляры) ничем не отличается от любое другое развертывание IaaS — необходимо toomonitor что hello ОС и приложения hello — это и как их использовать hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="c6568-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="c6568-106">ЦП</span><span class="sxs-lookup"><span data-stu-id="c6568-106">CPU</span></span>
- <span data-ttu-id="c6568-107">Память</span><span class="sxs-lookup"><span data-stu-id="c6568-107">Memory</span></span>
- <span data-ttu-id="c6568-108">пропускная способность сети;</span><span class="sxs-lookup"><span data-stu-id="c6568-108">Network bandwidth</span></span>
- <span data-ttu-id="c6568-109">Дисковое пространство</span><span class="sxs-lookup"><span data-stu-id="c6568-109">Disk space</span></span>

<span data-ttu-id="c6568-110">Виртуальные машины Azure должен toofigure перечисленных выше классов ресурсов hello достаточны или ли получить эти исчерпаны.</span><span class="sxs-lookup"><span data-stu-id="c6568-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="c6568-111">Вот более подробно на каждом из различных классов hello.</span><span class="sxs-lookup"><span data-stu-id="c6568-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="c6568-112">**Потребление ресурсов ЦП:** hello отношение, которое определено SAP для определенных рабочую нагрузку для HANA — принудительно toomake обязательно должен иметь достаточно ЦП ресурсы доступны toowork через hello данные, хранящиеся в памяти.</span><span class="sxs-lookup"><span data-stu-id="c6568-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="c6568-113">Тем не менее может возникнуть ситуация, где HANA выполняется дольше ЦП на выполнение запросов из-за toomissing индексы или аналогичные проблемы.</span><span class="sxs-lookup"><span data-stu-id="c6568-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="c6568-114">Это означает, что необходимо отслеживать потребление ресурсов ЦП hello HANA большом экземпляре единицы, а также ресурсов ЦП, потребляемых hello конкретными службами HANA.</span><span class="sxs-lookup"><span data-stu-id="c6568-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="c6568-115">**Потребление памяти:** является важным toomonitor из в HANA, а также за пределами HANA на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="c6568-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="c6568-116">В пределах HANA отслеживать как hello данных занимает место в выделенной памяти в toostay порядке в пределах hello необходимые размеры руководством по SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c6568-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="c6568-117">Также можно toomonitor потребление памяти на hello большом экземпляре уровня toomake том, что дополнительные установленные не HANA программного обеспечения не потребляют слишком много памяти и таким образом конкурируют HANA памяти.</span><span class="sxs-lookup"><span data-stu-id="c6568-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="c6568-118">**Пропускная способность сети:** hello шлюза виртуальной сети Azure имеет ограничения по пропускной способности данных, перемещение в hello виртуальной сети Azure, так бывает полезно toomonitor hello данных, полученных всеми hello Azure виртуальные машины в виртуальной сети toofigure, насколько близко являются ограничения toohello hello Azure номер SKU, выбранных для шлюза.</span><span class="sxs-lookup"><span data-stu-id="c6568-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="c6568-119">На устройстве HANA большом экземпляре hello он делает смысле toomonitor входящий и исходящий сетевой трафик также и отслеживания tookeep hello томов, которые выполняются со временем.</span><span class="sxs-lookup"><span data-stu-id="c6568-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="c6568-120">**Дисковое пространство.** Потребление дискового пространства обычно увеличивается с течением времени.</span><span class="sxs-lookup"><span data-stu-id="c6568-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="c6568-121">Это происходит по многим причинам, самые распространенные из которых — увеличение объема данных, создание резервных копий журнала транзакций, хранение файлов трассировки и выполнение моментальных снимков хранилища.</span><span class="sxs-lookup"><span data-stu-id="c6568-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="c6568-122">Таким образом является важным toomonitor использования места на диске и управлять дисковым пространством hello, связанный с единицей большом экземпляре HANA hello.</span><span class="sxs-lookup"><span data-stu-id="c6568-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="c6568-123">Мониторинг и устранение неполадок со стороны HANA</span><span class="sxs-lookup"><span data-stu-id="c6568-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="c6568-124">В порядке tooeffectively Анализ проблем связанных tooSAP HANA в Azure (большие экземпляры), очень полезно toonarrow вниз hello основную причину проблемы.</span><span class="sxs-lookup"><span data-stu-id="c6568-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="c6568-125">SAP опубликовала большой объем документации toohelp вы.</span><span class="sxs-lookup"><span data-stu-id="c6568-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="c6568-126">Применимые производительности HANA связанные tooSAP часто задаваемые вопросы можно найти в hello следующие примечания по SAP:</span><span class="sxs-lookup"><span data-stu-id="c6568-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- <span data-ttu-id="c6568-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Примечание SAP № 2222200. Часто задаваемые вопросы: сеть SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200)</span></span>
- <span data-ttu-id="c6568-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Примечание SAP № 2100040. Часто задаваемые вопросы: ЦП SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)</span></span>
- <span data-ttu-id="c6568-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 199997. Часто задаваемые вопросы: память SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064)</span></span>
- <span data-ttu-id="c6568-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Примечание SAP № 200000. Часто задаваемые вопросы: оптимизация производительности SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000)</span></span>
- <span data-ttu-id="c6568-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Примечание SAP № 199930. Часто задаваемые вопросы: анализ операций ввода-вывода SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930)</span></span>
- <span data-ttu-id="c6568-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 2177064. Часто задаваемые вопросы: перезапуск и сбои службы SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c6568-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064)</span></span>

<span data-ttu-id="c6568-133">**Оповещения SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="c6568-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="c6568-134">В качестве первого шага в журнале hello текущего SAP HANA предупреждения.</span><span class="sxs-lookup"><span data-stu-id="c6568-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="c6568-135">В SAP HANA Studio перейдите слишком**консоли администрирования: предупреждений: Показать: все предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="c6568-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="c6568-136">На этой вкладке будет показывать все предупреждения SAP HANA для конкретных значений (Свободная физическая память, ЦП, т. д.), которые выходят за пределы hello задать минимальное и максимальное пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="c6568-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="c6568-137">По умолчанию проверки автоматически обновляются каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="c6568-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![В SAP HANA Studio перейдите tooAdministration консоли: предупреждений: Показать: все оповещения](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="c6568-139">**ЦП**</span><span class="sxs-lookup"><span data-stu-id="c6568-139">**CPU**</span></span>

<span data-ttu-id="c6568-140">Для запуска из-за tooimproper порогового значения предупреждения разрешение является значение по умолчанию toohello tooreset или более рационального пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="c6568-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Значение по умолчанию toohello сброса или более рационального пороговое значение](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="c6568-142">Hello следующие оповещения могут указывать на проблемы ресурсов ЦП:</span><span class="sxs-lookup"><span data-stu-id="c6568-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="c6568-143">использование ЦП узла (оповещение 5);</span><span class="sxs-lookup"><span data-stu-id="c6568-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="c6568-144">последняя операция точки сохранения (оповещение 28);</span><span class="sxs-lookup"><span data-stu-id="c6568-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="c6568-145">длительность точки сохранения (оповещение 54).</span><span class="sxs-lookup"><span data-stu-id="c6568-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="c6568-146">Вы можете заметить высокую нагрузку на ЦП на базе данных SAP HANA из одного из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="c6568-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="c6568-147">для текущего использования ЦП или использования ЦП в прошлом возникает оповещение 5 (использование ЦП узла);</span><span class="sxs-lookup"><span data-stu-id="c6568-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="c6568-148">Hello ЦП отображаются на экране приветствия Обзор</span><span class="sxs-lookup"><span data-stu-id="c6568-148">hello displayed CPU usage on hello overview screen</span></span>

![На экране приветствия Обзор отображается ЦП](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="c6568-150">График нагрузки Hello могут отображаться высокую нагрузку на ЦП, или высокий уровень потребления в hello за последние:</span><span class="sxs-lookup"><span data-stu-id="c6568-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![граф нагрузки Hello может показывать высокий уровень загруженности ЦП или высокий уровень потребления hello за последние](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="c6568-152">Запускается из-за использования ЦП toohigh предупреждение может быть вызвано по нескольким причинам, включая, но не ограничиваясь: выполнения определенных операций, загрузку данных, зависание заданий, долго выполняющихся инструкций SQL и производительности неправильный запрос (например, с помощью BW на HANA кубы).</span><span class="sxs-lookup"><span data-stu-id="c6568-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="c6568-153">См. toohello [SAP HANA Устранение неполадок: вызывает, связанных с ЦП и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) сайта подробные шаги по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c6568-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c6568-154">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="c6568-154">**Operating System**</span></span>

<span data-ttu-id="c6568-155">Одним из наиболее важных hello проверяет для SAP HANA в Linux — toomake, что, отключены прозрачный огромный страниц см. в разделе [&#2131662; Примечание SAP — прозрачный огромный страниц (THP) на серверах SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="c6568-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="c6568-156">Можно проверить, разрешены ли прозрачный огромный страницы через следующую команду Linux hello: **классификатором /sys/kernel/mm/transparent\_hugepage или не включен**</span><span class="sxs-lookup"><span data-stu-id="c6568-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="c6568-157">Если _всегда_ заключается в квадратные скобки, как показано ниже, означает, включить hello прозрачный огромный страниц: [всегда] madvise никогда не; Если _никогда не_ заключено в квадратные скобки, как показано ниже, это означает, что hello прозрачный Огромный страницы отключены: всегда madvise [никогда не]</span><span class="sxs-lookup"><span data-stu-id="c6568-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="c6568-158">Hello следующую команду Linux должен возвращать ничего: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="c6568-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="c6568-159">Если _ulimit_ установлено, удалите его немедленно.</span><span class="sxs-lookup"><span data-stu-id="c6568-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="c6568-160">**Память**</span><span class="sxs-lookup"><span data-stu-id="c6568-160">**Memory**</span></span>

<span data-ttu-id="c6568-161">Можно заметить, что сумма hello памяти, выделенной с помощью hello SAP HANA базы данных больше, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="c6568-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="c6568-162">Hello следующие оповещения указывают на проблемы с большим объемом памяти использования:</span><span class="sxs-lookup"><span data-stu-id="c6568-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="c6568-163">использование физической памяти узла (оповещение 1);</span><span class="sxs-lookup"><span data-stu-id="c6568-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="c6568-164">использование памяти сервера доменных имен (оповещение 12);</span><span class="sxs-lookup"><span data-stu-id="c6568-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="c6568-165">общее использование памяти таблиц хранилища столбцов (оповещение 40);</span><span class="sxs-lookup"><span data-stu-id="c6568-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="c6568-166">использование памяти служб (оповещение 43);</span><span class="sxs-lookup"><span data-stu-id="c6568-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="c6568-167">использование памяти основного хранилища таблиц хранилища столбцов (оповещение 45);</span><span class="sxs-lookup"><span data-stu-id="c6568-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="c6568-168">файлы дампа среды выполнения (оповещение 46).</span><span class="sxs-lookup"><span data-stu-id="c6568-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="c6568-169">См. toohello [SAP HANA Устранение неполадок: проблем с памятью](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) сайта подробные шаги по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c6568-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c6568-170">**Сеть**</span><span class="sxs-lookup"><span data-stu-id="c6568-170">**Network**</span></span>

<span data-ttu-id="c6568-171">См. слишком[&#2081065; Примечание SAP — Устранение неполадок сети SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) и выполнять процедуры устранения неполадок в этой заметке SAP hello сети.</span><span class="sxs-lookup"><span data-stu-id="c6568-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="c6568-172">Анализ времени кругового пути между сервером и клиентом.</span><span class="sxs-lookup"><span data-stu-id="c6568-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="c6568-173">О.</span><span class="sxs-lookup"><span data-stu-id="c6568-173">A.</span></span> <span data-ttu-id="c6568-174">Запустить сценарий SQL hello [ _HANA\_сети\_клиенты_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="c6568-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="c6568-175">Выполните анализ обмена данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="c6568-175">Analyze internode communication.</span></span>
  <span data-ttu-id="c6568-176">О.</span><span class="sxs-lookup"><span data-stu-id="c6568-176">A.</span></span> <span data-ttu-id="c6568-177">Запустите скрипт SQL [ _HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="c6568-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="c6568-178">Выполните команду Linux **ifconfig** (hello вывода показывает, если выполняются какие-либо потери пакетов).</span><span class="sxs-lookup"><span data-stu-id="c6568-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="c6568-179">Выполните команду Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="c6568-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="c6568-180">Кроме того, используйте Привет открыть источник [IPERF](https://iperf.fr/) средства (или схожий) toomeasure реальной сети производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="c6568-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="c6568-181">Ссылки toohello [Устранение SAP HANA: производительность сети и проблем с подключением к](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) сайта подробные шаги по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c6568-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c6568-182">**Хранилище**</span><span class="sxs-lookup"><span data-stu-id="c6568-182">**Storage**</span></span>

<span data-ttu-id="c6568-183">С точки зрения конечного пользователя приложения (или hello системе в целом) работает медленно, не отвечает или даже может показаться toohang при возникновении проблем с производительностью ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c6568-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="c6568-184">В hello **тома** вкладку в SAP HANA Studio, вы увидите hello присоединенного тома и какие томов используются каждой службы.</span><span class="sxs-lookup"><span data-stu-id="c6568-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Hello вкладке тома в SAP HANA Studio можно увидеть hello присоединенного тома, а также какие тома используются всеми службами](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="c6568-186">Подключенные к нему тома в нижней части экрана приветствия, на котором вы увидите подробные сведения о hello hello тома, такие как файлы и статистику ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c6568-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Подключенные к нему тома в нижней части экрана приветствия, на котором вы увидите подробные сведения о hello hello тома, такие как файлы и статистику ввода-вывода](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="c6568-188">См. toohello [SAP HANA Устранение неполадок: операций ввода-вывода связанных основные причины и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) и [SAP HANA Устранение неполадок: диск связанных основные причины и решения](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) сайта подробные шаги по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c6568-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c6568-189">**Средства диагностики**</span><span class="sxs-lookup"><span data-stu-id="c6568-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="c6568-190">Выполните проверку работоспособности SAP HANA с помощью HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="c6568-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="c6568-191">Это средство возвращает потенциальные критические технические проблемы, которые должны вызвать оповещения в SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="c6568-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="c6568-192">См. слишком[&#1969700; Примечание SAP — коллекцию инструкций SQL для SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) и загрузите файл вложенного toothat hello SQL Statements.zip Примечание.</span><span class="sxs-lookup"><span data-stu-id="c6568-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="c6568-193">Сохраните этот ZIP-файл на локальный жесткий диск hello.</span><span class="sxs-lookup"><span data-stu-id="c6568-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="c6568-194">В Studio SAP HANA в hello **сведения о системе** щелкните правой кнопкой мыши в hello **имя** столбца и выберите команду **импорта инструкции SQL**.</span><span class="sxs-lookup"><span data-stu-id="c6568-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![В Studio SAP HANA, на вкладке hello системные сведения щелкните правой кнопкой мыши имя столбца hello и импорта инструкции SQL select](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="c6568-196">Файл SQL Statements.zip SELECT hello хранится локально, а папка с hello соответствующих инструкций SQL, которые будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="c6568-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="c6568-197">На этом этапе приветствия эти инструкции SQL могут выполняться много разных проверок диагностики.</span><span class="sxs-lookup"><span data-stu-id="c6568-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="c6568-198">Например, требования к пропускной способности tootest репликации системы SAP HANA, щелкните правой кнопкой мыши hello **пропускной способности** инструкции в разделе **репликации: пропускной способности** и выберите **откройте** в консоли SQL.</span><span class="sxs-lookup"><span data-stu-id="c6568-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="c6568-199">полную инструкцию SQL Hello открывает допускающему toobe входные параметры (раздел "изменения") изменен, а затем запускается.</span><span class="sxs-lookup"><span data-stu-id="c6568-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![Разрешает toobe входные параметры (раздел "изменения") изменен, а затем запускается открывает Hello полную инструкцию SQL](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="c6568-201">Еще один пример — щелкните правой кнопкой мыши на hello инструкции в разделе **репликации: Обзор**.</span><span class="sxs-lookup"><span data-stu-id="c6568-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="c6568-202">Выберите **Execute** hello контекстном меню:</span><span class="sxs-lookup"><span data-stu-id="c6568-202">Select **Execute** from hello context menu:</span></span>

![Еще один пример — щелкните правой кнопкой мыши в инструкциях hello в группе репликации: Обзор.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="c6568-205">После этого отобразятся сведения, которые помогут в устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="c6568-205">This results in information that helps with troubleshooting:</span></span>

![После этого отобразятся сведения, которые помогут в устранении неполадок](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="c6568-207">Здравствуйте, одинаково для HANA\_конфигурации\_Minichecks и установите флажок для любого _X_ метки в hello _C_ столбца (критический).</span><span class="sxs-lookup"><span data-stu-id="c6568-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="c6568-208">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="c6568-208">Sample outputs:</span></span>

<span data-ttu-id="c6568-209">**HANA\_Configuration\_MiniChecks\_Rev102.01 + 1** для общих проверок SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c6568-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01 + 1 для общих проверок SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="c6568-211">**HANA\_Services\_Overview** для получения общих сведений о том, какие службы SAP HANA запущены в данный момент.</span><span class="sxs-lookup"><span data-stu-id="c6568-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview для получения общих сведений о том, какие службы SAP HANA запущены в данный момент](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="c6568-213">**HANA\_Services\_Statistics** для получения сведений о службе SAP HANA (ЦП, память и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c6568-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="c6568-214">HANA\_Services\_Statistics для получения сведений о службе SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c6568-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="c6568-215">**HANA\_конфигурации\_Обзор\_Rev110 +** Общие сведения об экземпляре SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="c6568-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_конфигурации\_Обзор\_Rev110 + Общие сведения об экземпляре SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="c6568-217">**HANA\_конфигурации\_параметры\_Rev70 +** toocheck параметров SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c6568-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_конфигурации\_параметры\_Rev70 + toocheck параметров SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

