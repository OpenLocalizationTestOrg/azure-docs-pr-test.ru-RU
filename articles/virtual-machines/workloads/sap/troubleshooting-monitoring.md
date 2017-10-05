---
title: "Устранение неполадок и мониторинг архитектуры решения \"SAP HANA в Azure (крупные экземпляры)\" | Документация Майкрософт"
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
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="caa13-103">Как устранять неполадки и отслеживать работу SAP HANA (крупные экземпляры) в Azure</span><span class="sxs-lookup"><span data-stu-id="caa13-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="caa13-104">Мониторинг архитектуры SAP HANA в Azure (крупные экземпляры)</span><span class="sxs-lookup"><span data-stu-id="caa13-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="caa13-105">SAP HANA в Azure (крупные экземпляры) ничем не отличается от любого другого развертывания IaaS — необходимо отслеживать работу ОС и приложений, а также потребление следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="caa13-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="caa13-106">ЦП</span><span class="sxs-lookup"><span data-stu-id="caa13-106">CPU</span></span>
- <span data-ttu-id="caa13-107">Память</span><span class="sxs-lookup"><span data-stu-id="caa13-107">Memory</span></span>
- <span data-ttu-id="caa13-108">пропускная способность сети;</span><span class="sxs-lookup"><span data-stu-id="caa13-108">Network bandwidth</span></span>
- <span data-ttu-id="caa13-109">Дисковое пространство</span><span class="sxs-lookup"><span data-stu-id="caa13-109">Disk space</span></span>

<span data-ttu-id="caa13-110">Как и с виртуальными машинами Azure, необходимо выяснить, достаточно ли перечисленных выше классов ресурсов или они будут исчерпаны.</span><span class="sxs-lookup"><span data-stu-id="caa13-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="caa13-111">Ниже представлены подробные сведения о каждом классе.</span><span class="sxs-lookup"><span data-stu-id="caa13-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="caa13-112">**Потребление ресурсов ЦП.** Соотношение, определенное SAP для определенной рабочей нагрузки на HANA, применяется для обеспечения достаточного объема ресурсов ЦП, доступных для работы с данными, которые хранятся в памяти.</span><span class="sxs-lookup"><span data-stu-id="caa13-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="caa13-113">Тем не менее возможны ситуации, когда при выполнении запросов HANA потребляет много ресурсов ЦП из-за отсутствия индексов или подобных проблем.</span><span class="sxs-lookup"><span data-stu-id="caa13-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="caa13-114">Это означает, что необходимо отслеживать потребление ресурсов ЦП единицами крупных экземпляров HANA, а также ресурсов ЦП, используемых определенными службами HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="caa13-115">**Потребление памяти.** Важно выполнять мониторинг единицы как в HANA, так и за ее пределами.</span><span class="sxs-lookup"><span data-stu-id="caa13-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="caa13-116">В HANA отслеживайте потребление данными выделенной памяти, чтобы выполнялись требования к размеру, установленные SAP.</span><span class="sxs-lookup"><span data-stu-id="caa13-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="caa13-117">Кроме того, можно отслеживать потребление памяти на уровне крупных экземпляров, чтобы убедиться в том, что дополнительное установленное программное обеспечение, не относящееся к HANA, не потребляет слишком много памяти и, следовательно, не конкурирует с HANA за ресурсы памяти.</span><span class="sxs-lookup"><span data-stu-id="caa13-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="caa13-118">**Пропускная способность сети.** Пропускная способность шлюза виртуальной сети Azure при перемещении данных в виртуальную сеть Azure ограничена, поэтому полезно отслеживать данные, полученные виртуальными машинами Azure в виртуальной сети, чтобы выяснить, не превышены ли ограничения выбранного SKU шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="caa13-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="caa13-119">В единице крупного экземпляра HANA есть смысл отслеживать входящий и исходящий сетевой трафик, а также время от времени отслеживать обрабатываемые объемы.</span><span class="sxs-lookup"><span data-stu-id="caa13-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="caa13-120">**Дисковое пространство.** Потребление дискового пространства обычно увеличивается с течением времени.</span><span class="sxs-lookup"><span data-stu-id="caa13-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="caa13-121">Это происходит по многим причинам, самые распространенные из которых — увеличение объема данных, создание резервных копий журнала транзакций, хранение файлов трассировки и выполнение моментальных снимков хранилища.</span><span class="sxs-lookup"><span data-stu-id="caa13-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="caa13-122">Поэтому важно отслеживать использование дискового пространства и управлять дисковым пространством, связанным с единицей крупного экземпляра HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="caa13-123">Мониторинг и устранение неполадок со стороны HANA</span><span class="sxs-lookup"><span data-stu-id="caa13-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="caa13-124">Чтобы эффективно анализировать проблемы, связанные с SAP HANA в Azure (крупные экземпляры), полезно сузить круг возможных причин проблемы.</span><span class="sxs-lookup"><span data-stu-id="caa13-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="caa13-125">Компания SAP опубликовала огромное количество справочных материалов, которые могут вам помочь.</span><span class="sxs-lookup"><span data-stu-id="caa13-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="caa13-126">Ответы на часто задаваемые вопросы, связанные с производительностью SAP HANA, можно найти в следующих примечаниях SAP:</span><span class="sxs-lookup"><span data-stu-id="caa13-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- <span data-ttu-id="caa13-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Примечание SAP № 2222200. Часто задаваемые вопросы: сеть SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200)</span></span>
- <span data-ttu-id="caa13-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Примечание SAP № 2100040. Часто задаваемые вопросы: ЦП SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)</span></span>
- <span data-ttu-id="caa13-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 199997. Часто задаваемые вопросы: память SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064)</span></span>
- <span data-ttu-id="caa13-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Примечание SAP № 200000. Часто задаваемые вопросы: оптимизация производительности SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000)</span></span>
- <span data-ttu-id="caa13-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Примечание SAP № 199930. Часто задаваемые вопросы: анализ операций ввода-вывода SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930)</span></span>
- <span data-ttu-id="caa13-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Примечание SAP № 2177064. Часто задаваемые вопросы: перезапуск и сбои службы SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="caa13-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064)</span></span>

<span data-ttu-id="caa13-133">**Оповещения SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="caa13-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="caa13-134">Для начала проверьте текущие журналы оповещений SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="caa13-135">В SAP HANA Studio выберите **Administration Console: Alerts: Show: all alerts** (Консоль администрирования: Оповещения: Показать: Все оповещения).</span><span class="sxs-lookup"><span data-stu-id="caa13-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="caa13-136">На этой вкладке показаны все оповещения SAP HANA для определенных значений (объем свободной физической памяти, ЦП и т. д.), которые выходят за пределы установленных минимальных и максимальных пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="caa13-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="caa13-137">По умолчанию проверки автоматически обновляются каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="caa13-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![В SAP HANA Studio выберите Administration Console: Alerts: Show: all alerts (Консоль администрирования: Оповещения: Показать: Все оповещения).](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="caa13-139">**ЦП**</span><span class="sxs-lookup"><span data-stu-id="caa13-139">**CPU**</span></span>

<span data-ttu-id="caa13-140">Если оповещение запускается из-за неправильно заданного порогового значения, восстановите значение по умолчанию или задайте приемлемое пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="caa13-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Восстановление значения по умолчанию или задание приемлемого порогового значения](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="caa13-142">Следующие оповещения могут указывать на проблемы с ресурсами ЦП:</span><span class="sxs-lookup"><span data-stu-id="caa13-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="caa13-143">использование ЦП узла (оповещение 5);</span><span class="sxs-lookup"><span data-stu-id="caa13-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="caa13-144">последняя операция точки сохранения (оповещение 28);</span><span class="sxs-lookup"><span data-stu-id="caa13-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="caa13-145">длительность точки сохранения (оповещение 54).</span><span class="sxs-lookup"><span data-stu-id="caa13-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="caa13-146">Высокое потребление ресурсов ЦП в базе данных SAP HANA можно заметить по одному из следующих признаков:</span><span class="sxs-lookup"><span data-stu-id="caa13-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="caa13-147">для текущего использования ЦП или использования ЦП в прошлом возникает оповещение 5 (использование ЦП узла);</span><span class="sxs-lookup"><span data-stu-id="caa13-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="caa13-148">отображаемое потребление ресурсов ЦП на экране обзора.</span><span class="sxs-lookup"><span data-stu-id="caa13-148">The displayed CPU usage on the overview screen</span></span>

![Отображаемое потребление ресурсов ЦП на экране обзора](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="caa13-150">На графике Load (Нагрузка) может быть показан высокий уровень потребления ресурсов ЦП или высокий уровень потребления в прошлом.</span><span class="sxs-lookup"><span data-stu-id="caa13-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![На графике Load (Нагрузка) может быть показан высокий уровень потребления ресурсов ЦП или высокий уровень потребления в прошлом](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="caa13-152">Оповещение, возникшее из-за высокой загрузки ЦП, могло быть вызвано несколькими причинами, включая, помимо прочего, выполнение определенных операций, загрузку данных, зависание заданий, долго выполняющиеся инструкции SQL и снижение производительности запросов (например, при использовании кубов BW или HANA).</span><span class="sxs-lookup"><span data-stu-id="caa13-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="caa13-153">Подробные инструкции по устранению неполадок см. в разделе [CPU Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) (Основные причины проблем с ЦП и их решения) на сайте SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="caa13-154">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="caa13-154">**Operating System**</span></span>

<span data-ttu-id="caa13-155">Сведения об одной из самых важных проверок SAP HANA на Linux, которая заключается в проверке того, отключены ли Transparent Huge Pages ("прозрачные страницы"), см. в примечании [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662) (Примечание SAP № 2131662. Transparent Huge Pages (THP) на серверах SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="caa13-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="caa13-156">Проверить, включены ли Transparent Huge Pages, можно с помощью команды Linux: **cat /sys/kernel/mm/transparent\_hugepage/enabled**.</span><span class="sxs-lookup"><span data-stu-id="caa13-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="caa13-157">Если _always_ заключено в квадратные скобки, как показано ниже, это означает, что Transparent Huge Pages включены: [always] madvise never. Если _never_ заключено в квадратные скобки, как показано ниже, это означает, что Transparent Huge Pages отключены: always madvise [never].</span><span class="sxs-lookup"><span data-stu-id="caa13-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="caa13-158">Следующая команда Linux не должна что-либо возвращать: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="caa13-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="caa13-159">Если _ulimit_ установлено, удалите его немедленно.</span><span class="sxs-lookup"><span data-stu-id="caa13-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="caa13-160">**Память**</span><span class="sxs-lookup"><span data-stu-id="caa13-160">**Memory**</span></span>

<span data-ttu-id="caa13-161">Вы можете заметить, что объем памяти, выделенный базой данных SAP HANA, выше, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="caa13-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="caa13-162">Следующие оповещения указывают на неполадки в связи с использованием большого объема памяти:</span><span class="sxs-lookup"><span data-stu-id="caa13-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="caa13-163">использование физической памяти узла (оповещение 1);</span><span class="sxs-lookup"><span data-stu-id="caa13-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="caa13-164">использование памяти сервера доменных имен (оповещение 12);</span><span class="sxs-lookup"><span data-stu-id="caa13-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="caa13-165">общее использование памяти таблиц хранилища столбцов (оповещение 40);</span><span class="sxs-lookup"><span data-stu-id="caa13-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="caa13-166">использование памяти служб (оповещение 43);</span><span class="sxs-lookup"><span data-stu-id="caa13-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="caa13-167">использование памяти основного хранилища таблиц хранилища столбцов (оповещение 45);</span><span class="sxs-lookup"><span data-stu-id="caa13-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="caa13-168">файлы дампа среды выполнения (оповещение 46).</span><span class="sxs-lookup"><span data-stu-id="caa13-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="caa13-169">Подробные инструкции по устранению неполадок см. в разделе [Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) (Проблемы с памятью) на сайте SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="caa13-170">**Сеть**</span><span class="sxs-lookup"><span data-stu-id="caa13-170">**Network**</span></span>

<span data-ttu-id="caa13-171">См. примечание [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) (Примечание SAP № 2081065. Устранение неполадок сети SAP HANA) и выполните действия по устранению неполадок сети, приведенные в этом примечании SAP.</span><span class="sxs-lookup"><span data-stu-id="caa13-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="caa13-172">Анализ времени кругового пути между сервером и клиентом.</span><span class="sxs-lookup"><span data-stu-id="caa13-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="caa13-173">О.</span><span class="sxs-lookup"><span data-stu-id="caa13-173">A.</span></span> <span data-ttu-id="caa13-174">Запустите скрипт SQL [ _HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="caa13-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="caa13-175">Выполните анализ обмена данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="caa13-175">Analyze internode communication.</span></span>
  <span data-ttu-id="caa13-176">О.</span><span class="sxs-lookup"><span data-stu-id="caa13-176">A.</span></span> <span data-ttu-id="caa13-177">Запустите скрипт SQL [ _HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="caa13-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="caa13-178">Выполните команду Linux **ifconfig** (в выходных данных показано, есть ли какие-либо потери пакетов).</span><span class="sxs-lookup"><span data-stu-id="caa13-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="caa13-179">Выполните команду Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="caa13-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="caa13-180">Кроме того, используйте инструмент с открытым исходным кодом [IPERF](https://iperf.fr/) (или что-то похожее), чтобы измерить реальную производительность сети приложения.</span><span class="sxs-lookup"><span data-stu-id="caa13-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="caa13-181">Подробные инструкции по устранению неполадок см. в разделе [Network Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) (Проблемы с производительностью сети и подключением) на сайте SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="caa13-182">**Хранилище**</span><span class="sxs-lookup"><span data-stu-id="caa13-182">**Storage**</span></span>

<span data-ttu-id="caa13-183">С точки зрения конечного пользователя при наличии проблем с производительностью операций ввода-вывода приложение (либо система в целом) работает медленно, не отвечает или может даже зависнуть.</span><span class="sxs-lookup"><span data-stu-id="caa13-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="caa13-184">На вкладке **Volumes** (Тома) в SAP HANA Studio отображаются подключенные тома, а также то, какие тома использует каждая служба.</span><span class="sxs-lookup"><span data-stu-id="caa13-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![На вкладке Volumes (Тома) в SAP HANA Studio отображаются подключенные тома, а также то, какие тома использует каждая служба](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="caa13-186">В подключенных томах в нижней части экрана можно просматривать сведения о томах, например о файлах и статистике операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="caa13-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![В подключенных томах в нижней части экрана можно просматривать сведения о томах, например о файлах и статистике операций ввода-вывода](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="caa13-188">Подробные инструкции по устранению неполадок см. в разделах [I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) (Основные причины проблем с операциями ввода-вывода и их решения) и [Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) (Основные причины проблем с диском и их решения) на сайте SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="caa13-189">**Средства диагностики**</span><span class="sxs-lookup"><span data-stu-id="caa13-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="caa13-190">Выполните проверку работоспособности SAP HANA с помощью HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="caa13-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="caa13-191">Это средство возвращает потенциальные критические технические проблемы, которые должны вызвать оповещения в SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="caa13-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="caa13-192">См. примечание [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) (Примечание SAP № 1969700. Коллекция инструкций SQL для SAP HANA) и скачайте файл SQL Statements.zip, прикрепленный к этому примечанию.</span><span class="sxs-lookup"><span data-stu-id="caa13-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="caa13-193">Сохраните этот ZIP-файл на локальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="caa13-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="caa13-194">В SAP HANA Studio на вкладке **System Information** (Сведения о системе) щелкните правой кнопкой мыши столбец **Name** (Имя) и выберите **Import SQL Statements** (Импорт инструкций SQL).</span><span class="sxs-lookup"><span data-stu-id="caa13-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![В SAP HANA Studio на вкладке System Information (Сведения о системе) щелкните правой кнопкой мыши столбец Name (Имя) и выберите Import SQL Statements (Импорт инструкций SQL)](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="caa13-196">Выберите файл SQL Statements.zip, хранящийся локально, после чего будет импортирована папка с соответствующими инструкциями SQL.</span><span class="sxs-lookup"><span data-stu-id="caa13-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="caa13-197">На этом этапе с помощью этих инструкций SQL можно выполнить множество различных диагностических проверок.</span><span class="sxs-lookup"><span data-stu-id="caa13-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="caa13-198">Например, чтобы проверить требования к пропускной способности при репликации системы SAP HANA, щелкните правой кнопкой мыши инструкцию **Bandwidth** (Пропускная способность), выбрав **Replication: Bandwidth** (Репликация: Пропускная способность), и щелкните **Open** (Открыть) в консоли SQL.</span><span class="sxs-lookup"><span data-stu-id="caa13-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="caa13-199">Откроется полная инструкция SQL, что позволит изменить входные параметры (раздел изменения), а затем выполнить их.</span><span class="sxs-lookup"><span data-stu-id="caa13-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![Откроется полная инструкция SQL, что позволит изменить входные параметры (раздел изменения), а затем выполнить их](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="caa13-201">Другой пример — щелкнуть правой кнопкой мыши инструкции, выбрав **Replication: Overview** (Репликация: Обзор).</span><span class="sxs-lookup"><span data-stu-id="caa13-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="caa13-202">В контекстном меню выберите **Execute** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="caa13-202">Select **Execute** from the context menu:</span></span>

![Другой пример — щелкнуть правой кнопкой мыши инструкции, выбрав Replication: Overview (Репликация: Обзор).](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="caa13-205">После этого отобразятся сведения, которые помогут в устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="caa13-205">This results in information that helps with troubleshooting:</span></span>

![После этого отобразятся сведения, которые помогут в устранении неполадок](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="caa13-207">Сделайте то же самое для HANA\_Configuration\_Minichecks и проверьте наличие любых меток _X_ в столбце _C_ (Критический).</span><span class="sxs-lookup"><span data-stu-id="caa13-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="caa13-208">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="caa13-208">Sample outputs:</span></span>

<span data-ttu-id="caa13-209">**HANA\_Configuration\_MiniChecks\_Rev102.01 + 1** для общих проверок SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01 + 1 для общих проверок SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="caa13-211">**HANA\_Services\_Overview** для получения общих сведений о том, какие службы SAP HANA запущены в данный момент.</span><span class="sxs-lookup"><span data-stu-id="caa13-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview для получения общих сведений о том, какие службы SAP HANA запущены в данный момент](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="caa13-213">**HANA\_Services\_Statistics** для получения сведений о службе SAP HANA (ЦП, память и т. д.).</span><span class="sxs-lookup"><span data-stu-id="caa13-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="caa13-214">HANA\_Services\_Statistics для получения сведений о службе SAP HANA</span><span class="sxs-lookup"><span data-stu-id="caa13-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="caa13-215">**HANA\_Configuration\_Overview\_Rev110 +** для получения общих сведений об экземпляре SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110 + для получения общих сведений об экземпляре SAP HANA](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="caa13-217">**HANA\_Configuration\_Parameters\_Rev70 +** для проверки параметров SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="caa13-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70 + для проверки параметров SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

