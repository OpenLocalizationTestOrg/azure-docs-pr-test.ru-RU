---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="1dd77-101">Подключение компьютеров Linux к Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="1dd77-102">Log Analytics позволяет собирать и обрабатывать данные, созданные компьютерами Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="1dd77-103">Добавив данные, собранные с компьютера Linux, в OMS, вы можете управлять системами Linux и решениями контейнера, например Docker, практически из любого места.</span><span class="sxs-lookup"><span data-stu-id="1dd77-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="1dd77-104">Источники данных могут находиться в локальном центре обработки данных в качестве физических серверов, на виртуальных компьютерах в облачной службе, такой как Amazon Web Services (AWS) или Microsoft Azure, или даже на настольном ноутбуке.</span><span class="sxs-lookup"><span data-stu-id="1dd77-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="1dd77-105">Кроме того, OMS аналогичным образом собирает данные с компьютеров Windows. Так что это решение поддерживает гибридную ИТ-среду.</span><span class="sxs-lookup"><span data-stu-id="1dd77-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="1dd77-106">С помощью Log Analytics в OMS можно просматривать данные из всех этих источников и управлять ими на едином портале управления.</span><span class="sxs-lookup"><span data-stu-id="1dd77-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="1dd77-107">Поэтому вам не нужно отслеживать решение с помощью разных систем, его использование упрощается, а все необходимые данные можно экспортировать в любое существующее решение или систему бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="1dd77-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="1dd77-108">Эта статья представляет собой краткое руководство, которое поможет выполнить сбор данных и управлять ими на компьютерах Linux с помощью агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="1dd77-109">Дополнительные технические сведения, такие как конфигурация прокси-сервера, сведения о метриках CollectD и пользовательских источниках данных JSON, см. в [обзоре агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) и [полной документации по агенту OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="1dd77-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="1dd77-110">В настоящее время с компьютеров Linux можно собирать данные следующих типов:</span><span class="sxs-lookup"><span data-stu-id="1dd77-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="1dd77-111">Метрики производительности</span><span class="sxs-lookup"><span data-stu-id="1dd77-111">Performance metrics</span></span>
* <span data-ttu-id="1dd77-112">события системного журнала;</span><span class="sxs-lookup"><span data-stu-id="1dd77-112">Syslog events</span></span>
* <span data-ttu-id="1dd77-113">оповещения Nagios и Zabbix;</span><span class="sxs-lookup"><span data-stu-id="1dd77-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="1dd77-114">метрики производительности, данные инвентаризации и журналов контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="1dd77-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="1dd77-115">Поддерживаемые версии Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-115">Supported Linux versions</span></span>
<span data-ttu-id="1dd77-116">x86 и x64 являются официально поддерживаемыми версиями в различных дистрибутивах Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="1dd77-117">Однако агент OMS для Linux может выполняться и на других дистрибутивах, помимо следующих:</span><span class="sxs-lookup"><span data-stu-id="1dd77-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="1dd77-118">выпуски Amazon Linux 2012.09–2015.09;</span><span class="sxs-lookup"><span data-stu-id="1dd77-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="1dd77-119">CentOS Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="1dd77-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="1dd77-120">Oracle Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="1dd77-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="1dd77-121">сервер Red Hat Enterprise Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="1dd77-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="1dd77-122">Debian GNU/Linux 6, 7 и 8;</span><span class="sxs-lookup"><span data-stu-id="1dd77-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="1dd77-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10;</span><span class="sxs-lookup"><span data-stu-id="1dd77-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="1dd77-124">SUSE Linux Enterprise Server 11 и 12.</span><span class="sxs-lookup"><span data-stu-id="1dd77-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="1dd77-125">Агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-125">OMS Agent for Linux</span></span>
<span data-ttu-id="1dd77-126">Агент Operations Management Suite для Linux состоит из нескольких пакетов.</span><span class="sxs-lookup"><span data-stu-id="1dd77-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="1dd77-127">Файл выпуска содержит указанные ниже пакеты, к которым можно получить доступ, запустив пакет оболочки с помощью команды `--extract`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="1dd77-128">**Package**</span><span class="sxs-lookup"><span data-stu-id="1dd77-128">**Package**</span></span> | <span data-ttu-id="1dd77-129">**Версия**</span><span class="sxs-lookup"><span data-stu-id="1dd77-129">**Version**</span></span> | <span data-ttu-id="1dd77-130">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1dd77-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1dd77-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="1dd77-131">omsagent</span></span> |<span data-ttu-id="1dd77-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="1dd77-132">1.1.0</span></span> |<span data-ttu-id="1dd77-133">Агент Operations Management Suite для Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="1dd77-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="1dd77-134">omsconfig</span></span> |<span data-ttu-id="1dd77-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="1dd77-135">1.1.1</span></span> |<span data-ttu-id="1dd77-136">Агент конфигурации для агента OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="1dd77-137">omi</span><span class="sxs-lookup"><span data-stu-id="1dd77-137">omi</span></span> |<span data-ttu-id="1dd77-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="1dd77-138">1.0.8.3</span></span> |<span data-ttu-id="1dd77-139">OMI (Open Management Infrastructure) — упрощенная версия сервера CIM</span><span class="sxs-lookup"><span data-stu-id="1dd77-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="1dd77-140">scx</span><span class="sxs-lookup"><span data-stu-id="1dd77-140">scx</span></span> |<span data-ttu-id="1dd77-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="1dd77-141">1.6.2</span></span> |<span data-ttu-id="1dd77-142">Поставщики OMI CIM для метрик производительности операционной системы</span><span class="sxs-lookup"><span data-stu-id="1dd77-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="1dd77-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="1dd77-143">apache-cimprov</span></span> |<span data-ttu-id="1dd77-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1dd77-144">1.0.0</span></span> |<span data-ttu-id="1dd77-145">Поставщик мониторинга производительности сервера Apache HTTP Server для OMI.</span><span class="sxs-lookup"><span data-stu-id="1dd77-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="1dd77-146">Устанавливается только при обнаружении сервера Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="1dd77-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="1dd77-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="1dd77-147">mysql-cimprov</span></span> |<span data-ttu-id="1dd77-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1dd77-148">1.0.0</span></span> |<span data-ttu-id="1dd77-149">Поставщик мониторинга производительности сервера MySQL для OMI.</span><span class="sxs-lookup"><span data-stu-id="1dd77-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="1dd77-150">Устанавливается только при обнаружении сервера MySQL или MariaDB</span><span class="sxs-lookup"><span data-stu-id="1dd77-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="1dd77-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="1dd77-151">docker-cimprov</span></span> |<span data-ttu-id="1dd77-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="1dd77-152">0.1.0</span></span> |<span data-ttu-id="1dd77-153">Поставщик Docker для OMI.</span><span class="sxs-lookup"><span data-stu-id="1dd77-153">Docker provider for OMI.</span></span> <span data-ttu-id="1dd77-154">Устанавливается только при обнаружении Docker</span><span class="sxs-lookup"><span data-stu-id="1dd77-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="1dd77-155">Дополнительные артефакты установки</span><span class="sxs-lookup"><span data-stu-id="1dd77-155">Additional installation artifacts</span></span>
<span data-ttu-id="1dd77-156">После установки пакетов агента OMS для Linux применяются системные изменения конфигурации, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="1dd77-157">Эти артефакты удаляются после удаления пакета omsagent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="1dd77-158">Создается непривилегированный пользователь с именем `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="1dd77-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="1dd77-159">Это учетная запись, под которой запускается управляющая программа omsagent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="1dd77-160">Создается файл sudoers с директивами include в каталоге /etc/sudoers.d/omsagent. Таким образом пользователь omsagent получает право на перезапуск управляющих программ syslog и omsagent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="1dd77-161">Если директивы include sudo не поддерживаются в установленной версии sudo, эти записи будут записываться в каталог /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="1dd77-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="1dd77-162">Конфигурация системного журнала настраивается для перенаправления подмножества событий агенту.</span><span class="sxs-lookup"><span data-stu-id="1dd77-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="1dd77-163">Дополнительные сведения см. в разделе о **настройке сбора данных** ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="1dd77-164">Сведения о сборе данных Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-164">Linux data collection details</span></span>
<span data-ttu-id="1dd77-165">В следующей таблице содержатся методы сбора данных и другие связанные сведения.</span><span class="sxs-lookup"><span data-stu-id="1dd77-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="1dd77-166">источник</span><span class="sxs-lookup"><span data-stu-id="1dd77-166">source</span></span> | <span data-ttu-id="1dd77-167">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="1dd77-167">Direct Agent</span></span> | <span data-ttu-id="1dd77-168">Агент SCOM</span><span class="sxs-lookup"><span data-stu-id="1dd77-168">SCOM agent</span></span> | <span data-ttu-id="1dd77-169">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="1dd77-169">Azure Storage</span></span> | <span data-ttu-id="1dd77-170">Нужен ли SCOM?</span><span class="sxs-lookup"><span data-stu-id="1dd77-170">SCOM required?</span></span> | <span data-ttu-id="1dd77-171">Отправка данных агента SCOM через группу управления</span><span class="sxs-lookup"><span data-stu-id="1dd77-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="1dd77-172">Частота сбора</span><span class="sxs-lookup"><span data-stu-id="1dd77-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1dd77-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="1dd77-173">Zabbix</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1dd77-179">1 минута</span><span class="sxs-lookup"><span data-stu-id="1dd77-179">1 minute</span></span> |
| <span data-ttu-id="1dd77-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="1dd77-180">Nagios</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1dd77-186">При получении</span><span class="sxs-lookup"><span data-stu-id="1dd77-186">on arrival</span></span> |
| <span data-ttu-id="1dd77-187">syslog</span><span class="sxs-lookup"><span data-stu-id="1dd77-187">syslog</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1dd77-193">Из хранилища Azure — 10 минут, из агента — при получении</span><span class="sxs-lookup"><span data-stu-id="1dd77-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="1dd77-194">Счетчики производительности Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-194">Linux performance counters</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1dd77-200">По расписанию, не менее 10 секунд</span><span class="sxs-lookup"><span data-stu-id="1dd77-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="1dd77-201">Отслеживание изменений</span><span class="sxs-lookup"><span data-stu-id="1dd77-201">change tracking</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1dd77-207">Ежечасно</span><span class="sxs-lookup"><span data-stu-id="1dd77-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="1dd77-208">Требования к пакетам</span><span class="sxs-lookup"><span data-stu-id="1dd77-208">Package Requirements</span></span>
| <span data-ttu-id="1dd77-209">**Требуемый пакет**</span><span class="sxs-lookup"><span data-stu-id="1dd77-209">**Required package**</span></span> | <span data-ttu-id="1dd77-210">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1dd77-210">**Description**</span></span> | <span data-ttu-id="1dd77-211">**Минимальная версия**</span><span class="sxs-lookup"><span data-stu-id="1dd77-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1dd77-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="1dd77-212">Glibc</span></span> |<span data-ttu-id="1dd77-213">Библиотека C GNU</span><span class="sxs-lookup"><span data-stu-id="1dd77-213">GNU C library</span></span> |<span data-ttu-id="1dd77-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="1dd77-214">2.5-12</span></span> |
| <span data-ttu-id="1dd77-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="1dd77-215">Openssl</span></span> |<span data-ttu-id="1dd77-216">Библиотеки OpenSSL</span><span class="sxs-lookup"><span data-stu-id="1dd77-216">OpenSSL libraries</span></span> |<span data-ttu-id="1dd77-217">0.9.8e или 1.0</span><span class="sxs-lookup"><span data-stu-id="1dd77-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="1dd77-218">Curl</span><span class="sxs-lookup"><span data-stu-id="1dd77-218">Curl</span></span> |<span data-ttu-id="1dd77-219">Веб-клиент cURL</span><span class="sxs-lookup"><span data-stu-id="1dd77-219">cURL web client</span></span> |<span data-ttu-id="1dd77-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="1dd77-220">7.15.5</span></span> |
| <span data-ttu-id="1dd77-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="1dd77-221">Python-ctypes</span></span> |<span data-ttu-id="1dd77-222">Библиотеки функций</span><span class="sxs-lookup"><span data-stu-id="1dd77-222">function libraries</span></span> |<span data-ttu-id="1dd77-223">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1dd77-223">n/a</span></span> |
| <span data-ttu-id="1dd77-224">PAM</span><span class="sxs-lookup"><span data-stu-id="1dd77-224">PAM</span></span> |<span data-ttu-id="1dd77-225">Подключаемые модули аутентификации</span><span class="sxs-lookup"><span data-stu-id="1dd77-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="1dd77-226">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1dd77-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="1dd77-227">Для сбора сообщений системного журнала требуется rsyslog или syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="1dd77-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="1dd77-228">Управляющая программа syslog по умолчанию не поддерживается для сбора событий системного журнала в Red Hat Enterprise Linux версии 5, CentOS и Oracle Linux (sysklog).</span><span class="sxs-lookup"><span data-stu-id="1dd77-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="1dd77-229">Чтобы собирать данные системного журнала из дистрибутивов этих версий, требуется установить и настроить управляющую программу rsyslog, которая заменит sysklog.</span><span class="sxs-lookup"><span data-stu-id="1dd77-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="1dd77-230">Быстрая установка</span><span class="sxs-lookup"><span data-stu-id="1dd77-230">Quick install</span></span>
<span data-ttu-id="1dd77-231">Выполните следующие команды, чтобы скачать omsagent, проверить контрольную сумму, а также установить и внедрить агент.</span><span class="sxs-lookup"><span data-stu-id="1dd77-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="1dd77-232">Команды предназначены для 64-разрядных систем.</span><span class="sxs-lookup"><span data-stu-id="1dd77-232">Commands are for 64-bit.</span></span> <span data-ttu-id="1dd77-233">Идентификатор рабочей области и первичный ключ можно найти на портале OMS в разделе **Параметры** на вкладке **Подключенные источники**.</span><span class="sxs-lookup"><span data-stu-id="1dd77-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![сведения о рабочей области](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="1dd77-235">Существует множество других методов установки и обновления агента.</span><span class="sxs-lookup"><span data-stu-id="1dd77-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="1dd77-236">Дополнительные сведения об этих методах см. в разделе об [установке агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="1dd77-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="1dd77-237">Кроме того, можно просмотреть [видеоруководство Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="1dd77-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="1dd77-238">Выбор метода сбора данных Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="1dd77-239">Выбор типов данных для сбора зависит от того, хотите ли вы использовать портал OMS или изменять различные файлы конфигурации непосредственно в клиентах Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="1dd77-240">Если вы решили использовать портал, конфигурация автоматически отправляется на все клиентские компьютеры Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="1dd77-241">Если требуются различные конфигурации для различных клиентов Linux, клиентские файлы потребуется изменять по отдельности или воспользоваться альтернативным вариантом, например средствами PowerShell DSC, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="1dd77-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="1dd77-242">События системного журнала и счетчиков производительности, данные которых нужно собирать, можно указать с помощью файлов конфигурации на компьютерах Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="1dd77-243">*Выбрав настройку сбора данных путем изменения файлов конфигурации агента, следует отключить централизованную конфигурацию.*</span><span class="sxs-lookup"><span data-stu-id="1dd77-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="1dd77-244">Ниже представлены инструкции по настройке сбора данных в файлах конфигурации агента, а также по отключению центральной конфигурации для всех агентов OMS для Linux или отдельных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1dd77-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="1dd77-245">Отключение управления OMS для отдельного компьютера Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="1dd77-246">Централизованный сбор данных конфигурации для отдельного компьютера Linux отключается с помощью скрипта OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="1dd77-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="1dd77-247">Это может быть полезно, если подмножеству компьютеров требуется специальная конфигурация.</span><span class="sxs-lookup"><span data-stu-id="1dd77-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="1dd77-248">Чтобы отключить централизованную конфигурацию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1dd77-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="1dd77-249">Чтобы включить централизованную конфигурацию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1dd77-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="1dd77-250">Счетчики производительности Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-250">Linux performance counters</span></span>
<span data-ttu-id="1dd77-251">Счетчики производительности Linux функционируют подобно счетчикам производительности Windows.</span><span class="sxs-lookup"><span data-stu-id="1dd77-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="1dd77-252">Чтобы добавить и настроить их, можно использовать шаги, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="1dd77-253">После добавления счетчиков производительности в OMS сбор данных для них осуществляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="1dd77-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="1dd77-254">Добавление счетчиков производительности Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="1dd77-255">Чтобы настроить агенты OMS для Linux с помощью портала OMS, можно добавить счетчики производительности Linux на странице "Параметры" и щелкнуть **Данные**.</span><span class="sxs-lookup"><span data-stu-id="1dd77-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="1dd77-256">На странице **Параметры** в разделе **Данные** щелкните **Счетчики производительности Linux** и выберите или введите имя счетчика, который нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="1dd77-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="1dd77-257">![Данные](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="1dd77-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="1dd77-258">Если полное имя счетчика неизвестно, можно начать вводить часть имени, после чего отобразится список доступных счетчиков.</span><span class="sxs-lookup"><span data-stu-id="1dd77-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="1dd77-259">Найдя счетчик, который требуется добавить, щелкните его имя в списке и значок плюса.</span><span class="sxs-lookup"><span data-stu-id="1dd77-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="1dd77-260">После добавления счетчика он появляется в списке счетчиков, выделенный цветной линией.</span><span class="sxs-lookup"><span data-stu-id="1dd77-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="1dd77-261">По умолчанию установлен флажок **Apply below configuration to my machines** (Применить конфигурации ниже к моим компьютерам).</span><span class="sxs-lookup"><span data-stu-id="1dd77-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="1dd77-262">Если нужно отключить отправку данных конфигурации, снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="1dd77-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="1dd77-263">Изменив счетчики производительности, щелкните **Сохранить** в нижней части страницы для окончательной регистрации этих изменений.</span><span class="sxs-lookup"><span data-stu-id="1dd77-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="1dd77-264">Затем выполненные изменения конфигурации отправляются во все агенты OMS для Linux, зарегистрированные в OMS. Обычно это занимает 5 минут.</span><span class="sxs-lookup"><span data-stu-id="1dd77-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="1dd77-265">Настройка счетчиков производительности Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="1dd77-266">Для каждого счетчика производительности Windows можно выбрать конкретный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="1dd77-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="1dd77-267">Однако в случае счетчиков производительности Linux любой экземпляр выбранного счетчика применяется ко всем дочерним счетчикам родительского счетчика.</span><span class="sxs-lookup"><span data-stu-id="1dd77-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="1dd77-268">В следующей таблице представлены распространенные экземпляры для счетчиков производительности Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="1dd77-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="1dd77-269">**Имя экземпляра**</span><span class="sxs-lookup"><span data-stu-id="1dd77-269">**Instance name**</span></span> | <span data-ttu-id="1dd77-270">**Значение**</span><span class="sxs-lookup"><span data-stu-id="1dd77-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1dd77-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="1dd77-271">\_Total</span></span> |<span data-ttu-id="1dd77-272">Общее количество всех экземпляров</span><span class="sxs-lookup"><span data-stu-id="1dd77-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="1dd77-273">Все экземпляры</span><span class="sxs-lookup"><span data-stu-id="1dd77-273">All instances</span></span> |
| <span data-ttu-id="1dd77-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="1dd77-274">(/&#124;/var)</span></span> |<span data-ttu-id="1dd77-275">Сопоставление экземпляров с именем / или/var</span><span class="sxs-lookup"><span data-stu-id="1dd77-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="1dd77-276">Аналогичным образом, интервал выборки, выбранный для родительского счетчика, применяется ко всем дочерним счетчикам.</span><span class="sxs-lookup"><span data-stu-id="1dd77-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="1dd77-277">Другими словами, все интервалы выборки и экземпляры дочерних счетчиков связаны друг с другом.</span><span class="sxs-lookup"><span data-stu-id="1dd77-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="1dd77-278">Добавление и настройка метрик производительности в Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="1dd77-279">Собираемые метрики производительности определяются конфигурацией в файле /etc/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="1dd77-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="1dd77-280">Дополнительные сведения о доступных классах и метриках для агента OMS для Linux см. [здесь](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics).</span><span class="sxs-lookup"><span data-stu-id="1dd77-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="1dd77-281">Каждый объект или категорию метрики производительности для сбора следует определить в файле конфигурации в качестве одного элемента `<source>` .</span><span class="sxs-lookup"><span data-stu-id="1dd77-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="1dd77-282">Синтаксис соответствует шаблону ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="1dd77-283">Для этого элемента можно настроить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1dd77-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="1dd77-284">**Object\_name** — имя объекта в коллекции.</span><span class="sxs-lookup"><span data-stu-id="1dd77-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="1dd77-285">**Instance\_regex** — *регулярное выражение*, определяющее экземпляры, которые следует собирать.</span><span class="sxs-lookup"><span data-stu-id="1dd77-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="1dd77-286">Значение `.*` указывает все экземпляры.</span><span class="sxs-lookup"><span data-stu-id="1dd77-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="1dd77-287">Для сбора метрик процессора только для экземпляра \_Total можно указать `_Total`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="1dd77-288">Для сбора метрик обработки только для экземпляра crond или sshd можно указать `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="1dd77-289">**Counter\_name\_regex** — *регулярное выражение*, определяющее счетчики для сбора (для объекта).</span><span class="sxs-lookup"><span data-stu-id="1dd77-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="1dd77-290">Для сбора всех счетчиков для объекта укажите `.*`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="1dd77-291">Для сбора только счетчиков области подкачки для объекта памяти можно указать `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="1dd77-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="1dd77-292">**Interval**— частота сбора счетчиков объекта.</span><span class="sxs-lookup"><span data-stu-id="1dd77-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="1dd77-293">Конфигурация по умолчанию для метрики производительности:</span><span class="sxs-lookup"><span data-stu-id="1dd77-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="1dd77-294">Включение счетчиков производительности MySQL с помощью команд Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="1dd77-295">Если при установке пакета omsagent на компьютере обнаружен сервер MySQL или MariaDB, поставщик мониторинга производительности устанавливается автоматически для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="1dd77-296">Этот поставщик подключается к локальному серверу MySQL или MariaDB, чтобы предоставить статистику производительности.</span><span class="sxs-lookup"><span data-stu-id="1dd77-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="1dd77-297">Чтобы поставщик смог получить доступ к серверу MySQL, необходимо настроить учетные данные пользователя MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="1dd77-298">Чтобы определить учетную запись пользователя по умолчанию для сервера MySQL для localhost, используйте в качестве примера команду ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd77-299">Файл учетных данных должен быть доступен для чтения для учетной записи omsagent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="1dd77-300">Рекомендуется выполнить команду mycimprovauth, используя учетную запись omsgent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="1dd77-301">Кроме того, необходимые учетные данные MySQL можно указать в файле. Для этого создайте файл /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="1dd77-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="1dd77-302">Дополнительные сведения об управлении учетными данными MySQL для мониторинга с помощью файла mysql-auth см. в разделе [Управление учетными данными для мониторинга MySQL в файле аутентификации](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="1dd77-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="1dd77-303">Дополнительные сведения о разрешениях объектов, необходимых пользователю MySQL для сбора данных производительности сервера MySQL, см. в разделе [Разрешения базы данных, необходимые для счетчиков производительности MySQL](#database-permissions-required-for-mysql-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="1dd77-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="1dd77-304">Включение счетчиков производительности сервера Apache HTTP Server с помощью команд Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="1dd77-305">Если при установке пакета omsagent на компьютере обнаружен сервер Apache HTTP Server, для него автоматически устанавливается поставщик мониторинга производительности.</span><span class="sxs-lookup"><span data-stu-id="1dd77-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="1dd77-306">Этот поставщик использует модуль Apache, который нужно загрузить на сервер Apache HTTP Server для доступа к данным производительности.</span><span class="sxs-lookup"><span data-stu-id="1dd77-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="1dd77-307">Модуль можно загрузить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="1dd77-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="1dd77-308">Чтобы выгрузить модуль мониторинга Apache, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1dd77-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="1dd77-309">Просмотр данных производительности с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="1dd77-310">На портале Operations Management Suite щелкните плитку поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="1dd77-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="1dd77-311">В строке поиска введите `* (Type=Perf)` , чтобы просмотреть все счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="1dd77-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="1dd77-312">Так как OMS также собирает данные счетчика производительности Windows, следует ограничить область поиска данными Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="1dd77-313">В следующем примере приведены данные о производительности для сервера Linux с именем Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="1dd77-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![пример сервера, отображающийся на странице результатов поиска](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="1dd77-315">В результатах можно щелкнуть **Метрики** , чтобы просмотреть счетчики, для которых осуществлялся сбор данных.</span><span class="sxs-lookup"><span data-stu-id="1dd77-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="1dd77-316">Данные в реальном времени отображаются в виде графиков для каждого счетчика.</span><span class="sxs-lookup"><span data-stu-id="1dd77-316">Real-time data is shown as graphs for each counter.</span></span>

![Метрики](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="1dd77-318">syslog</span><span class="sxs-lookup"><span data-stu-id="1dd77-318">Syslog</span></span>
<span data-ttu-id="1dd77-319">Системный журнал — это протокол ведения журнала событий, аналогичный журналу событий Windows. При отображении в OMS они работают одинаково.</span><span class="sxs-lookup"><span data-stu-id="1dd77-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="1dd77-320">Добавление нового устройства системного журнала Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="1dd77-321">На странице **Параметры** на вкладке **Данные** щелкните раздел **Системный журнал** и слева от значка плюса введите имя устройства системного журнала, которое нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="1dd77-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="1dd77-322">![Системный журнал Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="1dd77-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="1dd77-323">Если полное имя устройства неизвестно, можно начать вводить часть имени, после чего отобразится список доступных устройств системного журнала.</span><span class="sxs-lookup"><span data-stu-id="1dd77-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="1dd77-324">Чтобы добавить найденное устройство системного журнала, щелкните его имя в списке, а затем — значок плюса.</span><span class="sxs-lookup"><span data-stu-id="1dd77-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="1dd77-325">После добавления устройства оно появляется в списке устройств, выделенное цветной линией.</span><span class="sxs-lookup"><span data-stu-id="1dd77-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="1dd77-326">Затем выберите степени серьезности (категории сведений устройства системного журнала) для сбора.</span><span class="sxs-lookup"><span data-stu-id="1dd77-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="1dd77-327">В нижней части страницы щелкните **Сохранить** для окончательной регистрации этих изменений.</span><span class="sxs-lookup"><span data-stu-id="1dd77-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="1dd77-328">Затем выполненные изменения конфигурации отправляются во все агенты OMS для Linux, зарегистрированные в OMS. Обычно это занимает 5 минут.</span><span class="sxs-lookup"><span data-stu-id="1dd77-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="1dd77-329">Настройка устройств системного журнала Linux в Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="1dd77-330">События системного журнала отправляются из управляющей программы syslog, например rsyslog или syslog-ng, в локальный порт, который прослушивает агент.</span><span class="sxs-lookup"><span data-stu-id="1dd77-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="1dd77-331">Порт по умолчанию — 25224.</span><span class="sxs-lookup"><span data-stu-id="1dd77-331">By default, port 25224.</span></span> <span data-ttu-id="1dd77-332">При установке агента применяется конфигурация системного журнала по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1dd77-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="1dd77-333">Ее можно найти в следующих каталогах:</span><span class="sxs-lookup"><span data-stu-id="1dd77-333">This is found at:</span></span>

<span data-ttu-id="1dd77-334">rsyslog — /etc/rsyslog.d/rsyslog-oms.conf;</span><span class="sxs-lookup"><span data-stu-id="1dd77-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="1dd77-335">syslog-ng — /etc/syslog-ng/syslog-ng.conf.</span><span class="sxs-lookup"><span data-stu-id="1dd77-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="1dd77-336">При конфигурации по умолчанию передаются события системного журнала агента OMS всех устройств с уровнем серьезности "Предупреждение" или выше.</span><span class="sxs-lookup"><span data-stu-id="1dd77-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd77-337">При изменении конфигурации системного журнала требуется перезапустить управляющую программу syslog, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="1dd77-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="1dd77-338">Ниже приведена конфигурация по умолчанию системного журнала для агента OMS для Linux для OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="1dd77-339">При использовании rsyslog:</span><span class="sxs-lookup"><span data-stu-id="1dd77-339">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="1dd77-340">При использовании syslog-ng:</span><span class="sxs-lookup"><span data-stu-id="1dd77-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="1dd77-341">Просмотр всех событий системного журнала с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="1dd77-342">На портале Operations Management Suite щелкните плитку **поиска по журналам** .</span><span class="sxs-lookup"><span data-stu-id="1dd77-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1dd77-343">В группе **Log Management** (Управление журналом) выберите предопределенный поиск по системному журналу, а затем — системный журнал, для которого требуется выполнить такой поиск.</span><span class="sxs-lookup"><span data-stu-id="1dd77-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="1dd77-344">В этом примере представлены все события системного журнала.</span><span class="sxs-lookup"><span data-stu-id="1dd77-344">This example shows all Syslog events.</span></span>

![события системного журнала, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="1dd77-346">Теперь вы можете подробно рассмотреть результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="1dd77-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="1dd77-347">Оповещения Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-347">Linux alerts</span></span>
<span data-ttu-id="1dd77-348">При использовании Nagios или Zabbix для управления компьютерами Linux OMS может получать оповещения, созданные с помощью этих средств.</span><span class="sxs-lookup"><span data-stu-id="1dd77-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="1dd77-349">Однако сейчас невозможно настроить данные входящих оповещений на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="1dd77-350">Вместо этого для отправки оповещений в OMS необходимо изменить файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1dd77-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="1dd77-351">Сбор оповещений из Nagios</span><span class="sxs-lookup"><span data-stu-id="1dd77-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="1dd77-352">Для сбора оповещений сервера Nagios необходимо внести следующие изменения в конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="1dd77-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="1dd77-353">Предоставьте пользователю **omsagent** доступ для чтения к файлу журнала Nagios (например, /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="1dd77-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="1dd77-354">Если файл nagios.log принадлежит группе **nagios**, пользователя **omsagent** можно добавить в группу **nagios**.</span><span class="sxs-lookup"><span data-stu-id="1dd77-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="1dd77-355">Измените файл конфигурации omsagent.conf (/etc/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="1dd77-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="1dd77-356">Для этого введите следующие записи в незакомментированном виде:</span><span class="sxs-lookup"><span data-stu-id="1dd77-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="1dd77-357">Перезапустите управляющую программу omsagent:</span><span class="sxs-lookup"><span data-stu-id="1dd77-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="1dd77-358">Сбор оповещений из Zabbix</span><span class="sxs-lookup"><span data-stu-id="1dd77-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="1dd77-359">Для сбора оповещений с сервера Zabbix выполните такие же действия, как и для Nagios выше, однако укажите имя пользователя и пароль в *текстовом виде*.</span><span class="sxs-lookup"><span data-stu-id="1dd77-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="1dd77-360">Это не очень удобно, но в скором времени это требование может измениться.</span><span class="sxs-lookup"><span data-stu-id="1dd77-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="1dd77-361">Чтобы устранить эту проблему, рекомендуется создать пользователя и предоставить ему разрешение только для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1dd77-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="1dd77-362">Раздел файла конфигурации omsagent.conf (/etc/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/conf/omsagent.conf) для Zabbix должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1dd77-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="1dd77-363">Просмотр оповещений с использованием поиска Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="1dd77-364">После настройки компьютеров Linux для отправки оповещений в OMS можно выбрать несколько простых запросов на поиск по журналу для просмотра оповещений.</span><span class="sxs-lookup"><span data-stu-id="1dd77-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="1dd77-365">В следующем примере запроса на поиск возвращаются все записанные созданные оповещения.</span><span class="sxs-lookup"><span data-stu-id="1dd77-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="1dd77-366">Например, если в ИТ-инфраструктуре возникает какая-либо проблема, ее источник можно определить по результатам в указанном ниже примере запроса.</span><span class="sxs-lookup"><span data-stu-id="1dd77-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="1dd77-367">Область исследования можно ограничить, просмотрев подробные сведения об оповещениях исходной системы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="1dd77-368">Преимущество заключается в том, что вам не нужно сначала просматривать различные системы управления при условии, что оповещения отправляются в OMS. Поиск можно начать прямо в этом решении.</span><span class="sxs-lookup"><span data-stu-id="1dd77-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="1dd77-369">Просмотр всех событий Nagios с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="1dd77-370">На портале Operations Management Suite щелкните плитку **поиска по журналам** .</span><span class="sxs-lookup"><span data-stu-id="1dd77-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1dd77-371">На панели запросов введите следующий запрос на поиск:</span><span class="sxs-lookup"><span data-stu-id="1dd77-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![оповещения Nagios, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="1dd77-373">Просмотрев результаты поиска, можно ознакомиться с дополнительными сведениями, например с *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="1dd77-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="1dd77-374">Просмотр всех событий Zabbix с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1dd77-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="1dd77-375">На портале Operations Management Suite щелкните плитку **поиска по журналам** .</span><span class="sxs-lookup"><span data-stu-id="1dd77-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1dd77-376">На панели запросов введите следующий запрос на поиск:</span><span class="sxs-lookup"><span data-stu-id="1dd77-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![оповещения Zabbix, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="1dd77-378">Просмотрев результаты поиска, можно ознакомиться с дополнительными сведениями, например с *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="1dd77-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="1dd77-379">Совместимость с System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="1dd77-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="1dd77-380">Агент OMS для Linux совместно использует двоичные файлы агента с агентом System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="1dd77-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="1dd77-381">При установке агента OMS для Linux в системе под управлением Operations Manager пакеты OMI и SCX на компьютере обновляются до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="1dd77-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="1dd77-382">Агент OMS для Linux и System Center 2012 R2 совместимы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="1dd77-383">Тем не менее **System Center 2012 SP1 и более ранние версии не совместимы с агентом OMS для Linux.**</span><span class="sxs-lookup"><span data-stu-id="1dd77-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="1dd77-384">Если агент OMS для Linux устанавливается на компьютер, которым в настоящее время не управляет Operations Manager, но такое управление требуется в будущем, нужно изменить конфигурацию OMI до обнаружения компьютера.</span><span class="sxs-lookup"><span data-stu-id="1dd77-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="1dd77-385">**Не нужно выполнять этот шаг, если агент Operations Manager установлен до агента OMS для Linux.**</span><span class="sxs-lookup"><span data-stu-id="1dd77-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="1dd77-386">Обеспечение взаимодействия агента OMS для Linux с Operations Manager</span><span class="sxs-lookup"><span data-stu-id="1dd77-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="1dd77-387">Измените файл /etc/opt/omi/conf/omiserver.conf.</span><span class="sxs-lookup"><span data-stu-id="1dd77-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="1dd77-388">Укажите для **httpsport=** номер порта 1270.</span><span class="sxs-lookup"><span data-stu-id="1dd77-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="1dd77-389">Таким образом — `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="1dd77-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="1dd77-390">Перезапустите сервер OMI, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1dd77-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="1dd77-391">Разрешения базы данных, необходимые для счетчиков производительности MySQL</span><span class="sxs-lookup"><span data-stu-id="1dd77-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="1dd77-392">Чтобы предоставить разрешения пользователю мониторинга MySQL, у пользователя, предоставляющего разрешения, должна быть привилегия с параметром GRANT, а также предоставляемая привилегия.</span><span class="sxs-lookup"><span data-stu-id="1dd77-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="1dd77-393">Чтобы пользователь MySQL смог возвращать данные о производительности, ему потребуется доступ к следующим запросам:</span><span class="sxs-lookup"><span data-stu-id="1dd77-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="1dd77-394">В дополнение к этим запросам пользователю MySQL необходим доступ с разрешением SELECT для следующих таблиц по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="1dd77-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="1dd77-395">information_schema;</span><span class="sxs-lookup"><span data-stu-id="1dd77-395">information_schema</span></span>
* <span data-ttu-id="1dd77-396">mysql</span><span class="sxs-lookup"><span data-stu-id="1dd77-396">mysql</span></span>

<span data-ttu-id="1dd77-397">Эти привилегии можно предоставить, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1dd77-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="1dd77-398">Управление учетными данными для мониторинга MySQL в файле аутентификации</span><span class="sxs-lookup"><span data-stu-id="1dd77-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="1dd77-399">В следующих разделах представлены инструкции по управлению учетными данными MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="1dd77-400">Настройка поставщика OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="1dd77-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="1dd77-401">Поставщику OMI MySQL требуется предварительно настроенный пользователь MySQL и установленные клиентские библиотеки MySQL, чтобы запрашивать сведения о производительности и состоянии из экземпляра MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="1dd77-402">Файл аутентификации OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="1dd77-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="1dd77-403">Поставщик OMI MySQL использует файл аутентификации, чтобы определить адрес привязки и порт, который прослушивает экземпляр MySQL, а также учетные данные, которые нужно использовать для сбора метрик.</span><span class="sxs-lookup"><span data-stu-id="1dd77-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="1dd77-404">Во время установки поставщик OMI MySQL проверит файлы конфигурации MySQL my.cnf (расположение по умолчанию) для адреса привязки и порта и частично укажет файл аутентификации OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="1dd77-405">Чтобы завершить мониторинг экземпляра сервера MySQL, добавьте предварительно созданный файл аутентификации OMI MySQL в соответствующий каталог.</span><span class="sxs-lookup"><span data-stu-id="1dd77-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="1dd77-406">Формат файла аутентификации</span><span class="sxs-lookup"><span data-stu-id="1dd77-406">Authentication file format</span></span>
<span data-ttu-id="1dd77-407">Файл аутентификации OMI MySQL — текстовый файл, содержащий следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="1dd77-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="1dd77-408">Порт</span><span class="sxs-lookup"><span data-stu-id="1dd77-408">Port</span></span>
* <span data-ttu-id="1dd77-409">адрес привязки;</span><span class="sxs-lookup"><span data-stu-id="1dd77-409">Bind-Address</span></span>
* <span data-ttu-id="1dd77-410">имя пользователя MySQL;</span><span class="sxs-lookup"><span data-stu-id="1dd77-410">MySQL username</span></span>
* <span data-ttu-id="1dd77-411">пароль в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1dd77-411">Base64 encoded password</span></span>

<span data-ttu-id="1dd77-412">Файл аутентификации OMI MySQL предоставляет привилегии только для чтения и записи для пользователя Linux, который создал его.</span><span class="sxs-lookup"><span data-stu-id="1dd77-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="1dd77-413">Файл аутентификации OMI MySQL по умолчанию содержит экземпляр по умолчанию и номер порта в зависимости от доступных сведений и данных, полученных в результате анализа найденного файла конфигурации MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="1dd77-414">Экземпляр по умолчанию позволяет упростить управление несколькими экземплярами MySQL на одном узле Linux. Он обозначается экземпляром с портом 0.</span><span class="sxs-lookup"><span data-stu-id="1dd77-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="1dd77-415">Все добавленные экземпляры наследуют свойства, заданные в экземпляре по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1dd77-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="1dd77-416">Например, при добавлении экземпляра MySQL, который прослушивает порт 3308, для его мониторинга будет использоваться адрес привязки, имя пользователя и пароль в кодировке Base64 экземпляра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1dd77-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="1dd77-417">Если экземпляр на порте 3308 привязан к другому адресу и использует те же имя пользователя и пароль MySQL, необходимо переопределить только адрес привязки, а другие свойства будут унаследованы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="1dd77-418">Содержание файлов аутентификации выглядит, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="1dd77-419">Экземпляр по умолчанию и экземпляр с портом 3308:</span><span class="sxs-lookup"><span data-stu-id="1dd77-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="1dd77-420">Экземпляр по умолчанию и экземпляр с портом 3308 и другим паролем в кодировке Base 64:</span><span class="sxs-lookup"><span data-stu-id="1dd77-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="1dd77-421">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="1dd77-421">**Property**</span></span> | <span data-ttu-id="1dd77-422">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1dd77-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1dd77-423">Порт</span><span class="sxs-lookup"><span data-stu-id="1dd77-423">Port</span></span> |<span data-ttu-id="1dd77-424">Это текущий порт, который прослушивает экземпляр MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="1dd77-425">Порт 0 означает, что для экземпляра по умолчанию используются следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="1dd77-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="1dd77-426">адрес привязки;</span><span class="sxs-lookup"><span data-stu-id="1dd77-426">Bind-Address</span></span> |<span data-ttu-id="1dd77-427">Это текущий адрес привязки MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="1dd77-428">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="1dd77-428">username</span></span> |<span data-ttu-id="1dd77-429">Это имя пользователя MySQL, которое нужно использовать для мониторинга экземпляра сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="1dd77-430">пароль в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1dd77-430">Base64 encoded Password</span></span> |<span data-ttu-id="1dd77-431">Это пароль пользователя мониторинга MySQL в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1dd77-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="1dd77-432">Автоматическое обновление</span><span class="sxs-lookup"><span data-stu-id="1dd77-432">AutoUpdate</span></span> |<span data-ttu-id="1dd77-433">При обновлении поставщик OMI MySQL повторно выполнит поиск изменений в файле my.cnf и перезапишет файл аутентификации OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="1dd77-434">Задайте для этого флага значение true или false в зависимости от необходимости обновления файла аутентификации OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="1dd77-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="1dd77-435">Расположение файла аутентификации</span><span class="sxs-lookup"><span data-stu-id="1dd77-435">Authentication file location</span></span>
<span data-ttu-id="1dd77-436">Файл аутентификации OMI MySQL должен называться mysql-auth и находиться в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="1dd77-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="1dd77-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="1dd77-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="1dd77-438">Файл (и каталог auth/omsagent) должен принадлежать пользователю omsagent.</span><span class="sxs-lookup"><span data-stu-id="1dd77-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="1dd77-439">Журналы агента</span><span class="sxs-lookup"><span data-stu-id="1dd77-439">Agent logs</span></span>
<span data-ttu-id="1dd77-440">Журналы агента OMS для Linux находятся в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="1dd77-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="1dd77-441">/var/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="1dd77-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="1dd77-442">Журналы агента OMS для Linux для программы omsconfig (конфигурация агента) расположены в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="1dd77-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="1dd77-443">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="1dd77-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="1dd77-444">Журналы для компонентов OMI и SCX (предоставляют данные метрики производительности) расположены в следующих каталогах:</span><span class="sxs-lookup"><span data-stu-id="1dd77-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="1dd77-445">/var/opt/omi/log/ и /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="1dd77-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="1dd77-446">Устранение неполадок, связанных с агентом OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="1dd77-447">Используйте следующие сведения для диагностики и устранения типичных неполадок.</span><span class="sxs-lookup"><span data-stu-id="1dd77-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="1dd77-448">Если предоставленные в этом разделе сведения не помогут, для решения проблем также можно использовать следующие источники:</span><span class="sxs-lookup"><span data-stu-id="1dd77-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="1dd77-449">Клиенты с поддержкой Premier могут обратиться в службу поддержки [здесь](https://premier.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1dd77-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="1dd77-450">Клиенты с соглашением на поддержку Azure могут обратиться в службу поддержки на [портале Azure](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="1dd77-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="1dd77-451">Можно [сообщить о проблеме в GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).</span><span class="sxs-lookup"><span data-stu-id="1dd77-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="1dd77-452">Можно воспользоваться форумом обратной связи для получения предложений и создания отчета об ошибках ([http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)).</span><span class="sxs-lookup"><span data-stu-id="1dd77-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="1dd77-453">Важные расположения журналов</span><span class="sxs-lookup"><span data-stu-id="1dd77-453">Important log locations</span></span>
| <span data-ttu-id="1dd77-454">Файл</span><span class="sxs-lookup"><span data-stu-id="1dd77-454">File</span></span> | <span data-ttu-id="1dd77-455">Путь</span><span class="sxs-lookup"><span data-stu-id="1dd77-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="1dd77-456">Файл журнала агента OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="1dd77-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="1dd77-457">Файл журнала конфигурации агента OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="1dd77-458">Важные файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="1dd77-458">Important configuration files</span></span>
| <span data-ttu-id="1dd77-459">Категория</span><span class="sxs-lookup"><span data-stu-id="1dd77-459">Catergory</span></span> | <span data-ttu-id="1dd77-460">Расположение файла</span><span class="sxs-lookup"><span data-stu-id="1dd77-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="1dd77-461">syslog</span><span class="sxs-lookup"><span data-stu-id="1dd77-461">Syslog</span></span> |<span data-ttu-id="1dd77-462">`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` или `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="1dd77-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="1dd77-463">Данные производительности, Nagios, Zabbix, выходные данные OMS и общая конфигурация агента</span><span class="sxs-lookup"><span data-stu-id="1dd77-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="1dd77-464">Дополнительные конфигурации</span><span class="sxs-lookup"><span data-stu-id="1dd77-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="1dd77-465">Если конфигурация портала OMS включена, при редактировании файлы конфигурации счетчиков производительности и системных журналов переопределяются.</span><span class="sxs-lookup"><span data-stu-id="1dd77-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="1dd77-466">Конфигурацию можно отключить для всех узлов (полностью) на портале OMS или для одного узла с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="1dd77-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="1dd77-467">Включение ведения журнала отладки</span><span class="sxs-lookup"><span data-stu-id="1dd77-467">Enable debug logging</span></span>
<span data-ttu-id="1dd77-468">Чтобы включить ведение журнала отладки, можно использовать подключаемый модуль выходных данных OMS и подробные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="1dd77-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="1dd77-469">Подключаемый модуль выходных данных OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-469">OMS output plugin</span></span>
<span data-ttu-id="1dd77-470">Подключаемый модуль позволяет указывать уровни ведения журнала для разных входных и выходных данных через FluentD.</span><span class="sxs-lookup"><span data-stu-id="1dd77-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="1dd77-471">Чтобы определить для выходных данных OMS другой уровень ведения журнала, измените общую конфигурацию агента в файле `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="1dd77-472">В нижней части файла конфигурации, измените значение свойства `log_level` с `info` на `debug`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="1dd77-473">Ведение журнала отладки позволяет просматривать групповые отправки данных в службу OMS по типу, количеству элементов данных и времени, затраченному на отправку.</span><span class="sxs-lookup"><span data-stu-id="1dd77-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="1dd77-474">*Пример включенного журнала отладки.*</span><span class="sxs-lookup"><span data-stu-id="1dd77-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="1dd77-475">Подробные выходные данные</span><span class="sxs-lookup"><span data-stu-id="1dd77-475">Verbose output</span></span>
<span data-ttu-id="1dd77-476">Вместо использования подключаемого модуля выходных данных OMS элементы данных можно отправлять непосредственно в `stdout`, который отображается в файле журнала агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="1dd77-477">В файле общей конфигурации агента OMS в разделе `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` закомментируйте подключаемый модуль выходных данных OMS, добавив в начало каждой строки символ `#`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="1dd77-478">В нижней части подключаемого модуля удалите комментарий в следующем разделе, удалив в начале каждой строки символ `#`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="1dd77-479">Перенаправленные сообщения системного журнала не отображаются в журнале</span><span class="sxs-lookup"><span data-stu-id="1dd77-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-480">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-480">Probable causes</span></span>
* <span data-ttu-id="1dd77-481">В конфигурации сервера Linux не включен сбор данных об отправленных средствах и (или) данных об уровнях ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1dd77-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="1dd77-482">Системный журнал не перенаправляется на сервер Linux должным образом.</span><span class="sxs-lookup"><span data-stu-id="1dd77-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="1dd77-483">Количество сообщений, перенаправленных за одну секунду, слишком большое и агент OMS для Linux не может их обработать.</span><span class="sxs-lookup"><span data-stu-id="1dd77-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-484">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-484">Resolutions</span></span>
* <span data-ttu-id="1dd77-485">Настройте на портале OMS все средства и правильные уровни ведения журнала, необходимые для системного журнала:</span><span class="sxs-lookup"><span data-stu-id="1dd77-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="1dd77-486">**OMS Portal (Портал OMS) > Параметры > Данные > Системный журнал**.</span><span class="sxs-lookup"><span data-stu-id="1dd77-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="1dd77-487">Настройте получение перенаправленных сообщений в управляющих программах обмена сообщениями системных журналов (`rsyslog`, `syslog-ng`).</span><span class="sxs-lookup"><span data-stu-id="1dd77-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="1dd77-488">Отключите блокировку сообщений в параметрах брандмауэра на сервере системного журнала.</span><span class="sxs-lookup"><span data-stu-id="1dd77-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="1dd77-489">Отправьте смоделированное сообщение системного журнала на портал OMS, используя команду `logger`, например:</span><span class="sxs-lookup"><span data-stu-id="1dd77-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="1dd77-490">Проблемы с подключением к OMS при использовании прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="1dd77-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-491">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-491">Probable causes</span></span>
* <span data-ttu-id="1dd77-492">Во время установки и настройки агента указан неправильный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1dd77-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="1dd77-493">Конечные точки службы OMS не включены в список разрешенных в вашем центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="1dd77-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-494">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-494">Resolutions</span></span>
* <span data-ttu-id="1dd77-495">Переустановите агент OMS для Linux, используя следующую команду с включенным параметром `-v`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="1dd77-496">За счет этого подробные выходные данные агента могут подключиться к службе OMS через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1dd77-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="1dd77-497">Просмотрите сведения для прокси-сервера OMS в разделе [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server) (Настройка агента для использования с прокси-сервером HTTP).</span><span class="sxs-lookup"><span data-stu-id="1dd77-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="1dd77-498">Добавьте следующие конечные точки службы OMS в список разрешенных.</span><span class="sxs-lookup"><span data-stu-id="1dd77-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="1dd77-499">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="1dd77-499">Agent Resource</span></span> | <span data-ttu-id="1dd77-500">порты;</span><span class="sxs-lookup"><span data-stu-id="1dd77-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="1dd77-501">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1dd77-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="1dd77-502">Порт 443</span><span class="sxs-lookup"><span data-stu-id="1dd77-502">Port 443</span></span> |
| <span data-ttu-id="1dd77-503">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1dd77-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="1dd77-504">Порт 443</span><span class="sxs-lookup"><span data-stu-id="1dd77-504">Port 443</span></span> |
| <span data-ttu-id="1dd77-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="1dd77-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="1dd77-506">Порт 443</span><span class="sxs-lookup"><span data-stu-id="1dd77-506">Port 443</span></span> |
| <span data-ttu-id="1dd77-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="1dd77-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="1dd77-508">Порт 443</span><span class="sxs-lookup"><span data-stu-id="1dd77-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="1dd77-509">При подключении отобразилась ошибка с кодом 403</span><span class="sxs-lookup"><span data-stu-id="1dd77-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-510">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-510">Probable causes</span></span>
* <span data-ttu-id="1dd77-511">На сервере Linux установлено неправильное время или дата.</span><span class="sxs-lookup"><span data-stu-id="1dd77-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="1dd77-512">Используется неправильный идентификатор или ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1dd77-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="1dd77-513">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="1dd77-513">Resolution</span></span>
* <span data-ttu-id="1dd77-514">Проверьте время на вашем сервере Linux с помощью команды `date`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="1dd77-515">Если время отличается больше или меньше чем на 15 минут от текущего времени, при подключении произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="1dd77-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="1dd77-516">Чтобы исправить это, обновите дату и (или) часовой пояс на сервере Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="1dd77-517">Агент OMS для Linux последней версии отправляет пользователям уведомление, если сбой подключения связан с разницей во времени.</span><span class="sxs-lookup"><span data-stu-id="1dd77-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="1dd77-518">Повторно установите подключение, используя правильный идентификатор и ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1dd77-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="1dd77-519">Дополнительные сведения см. в разделе [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Подключение с помощью командной строки).</span><span class="sxs-lookup"><span data-stu-id="1dd77-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="1dd77-520">После подключения в файле журнала отображается ошибка с кодом 500 или 404</span><span class="sxs-lookup"><span data-stu-id="1dd77-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="1dd77-521">Это известная проблема, возникающая во время передачи данных Linux в рабочую область OMS впервые.</span><span class="sxs-lookup"><span data-stu-id="1dd77-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="1dd77-522">Это не влияет на отправляемые данные и не вызывает другие проблемы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="1dd77-523">Во время первого подключения эти ошибки можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="1dd77-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="1dd77-524">Данные Nagios не отображаются на портале OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-525">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-525">Probable causes</span></span>
* <span data-ttu-id="1dd77-526">У пользователя omsagent отсутствуют разрешения на чтение данных в файле журнала Nagios.</span><span class="sxs-lookup"><span data-stu-id="1dd77-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="1dd77-527">В файле omsagent.conf для Nagios все еще закомментированы разделы source и filter.</span><span class="sxs-lookup"><span data-stu-id="1dd77-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-528">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-528">Resolutions</span></span>
* <span data-ttu-id="1dd77-529">Предоставьте пользователю omsagent разрешения на чтение файла Nagios.</span><span class="sxs-lookup"><span data-stu-id="1dd77-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="1dd77-530">Дополнительные сведения см. в разделе об [оповещениях Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts).</span><span class="sxs-lookup"><span data-stu-id="1dd77-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="1dd77-531">В файле общей конфигурации агента OMS для Linux в разделе `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` удалите комментарии для **разделов** Nagios source и filter, как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="1dd77-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="1dd77-532">Данные Linux не отображаются на портале OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-533">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-533">Probable causes</span></span>
* <span data-ttu-id="1dd77-534">Сбой при подключении к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="1dd77-535">Подключение к службе OMS заблокировано.</span><span class="sxs-lookup"><span data-stu-id="1dd77-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="1dd77-536">Создана резервная копия данных агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-537">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-537">Resolutions</span></span>
* <span data-ttu-id="1dd77-538">Проверьте подключение к службе OMS (должен быть создан файл `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`).</span><span class="sxs-lookup"><span data-stu-id="1dd77-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="1dd77-539">Повторно установите подключение, используя командную строку omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="1dd77-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="1dd77-540">Дополнительные сведения см. в разделе [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Подключение с помощью командной строки).</span><span class="sxs-lookup"><span data-stu-id="1dd77-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="1dd77-541">При использовании прокси-сервера выполните действия по устранению неполадок, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="1dd77-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="1dd77-542">В некоторых случаях сбой подключения между агентом OMS для Linux и порталом OMS связан с тем, что в буфере достигнут максимальный размер резервных копий данных агента (50 МБ).</span><span class="sxs-lookup"><span data-stu-id="1dd77-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="1dd77-543">Перезапустите агент OMS для Linux, выполнив команду `/opt/microsoft/omsagent/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="1dd77-544">Эта проблема исправлена в агенте версии 1.1.0-28 и выше.</span><span class="sxs-lookup"><span data-stu-id="1dd77-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="1dd77-545">Конфигурация счетчика производительности системного журнала Linux не применена на портале OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-546">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-546">Probable causes</span></span>
* <span data-ttu-id="1dd77-547">Агент конфигурации в агенте OMS для Linux не получил сведения о последней конфигурации с портала OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="1dd77-548">Измененные параметры не были применены на портале.</span><span class="sxs-lookup"><span data-stu-id="1dd77-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-549">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-549">Resolutions</span></span>
<span data-ttu-id="1dd77-550">Агент конфигурации `omsconfig` в агенте OMS для Linux извлекает сведения об изменениях конфигурации портала OMS каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="1dd77-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="1dd77-551">После этого эта конфигурация применяется к файлам конфигурации агента OMS для Linux, расположенным в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="1dd77-552">В некоторых случаях агент OMS для Linux не может взаимодействовать со службой конфигурации портала, в результате чего последние изменения не применяются.</span><span class="sxs-lookup"><span data-stu-id="1dd77-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="1dd77-553">Для агента `omsconfig` должны быть установлены следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1dd77-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="1dd77-554">`dpkg --list omsconfig` или `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="1dd77-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="1dd77-555">Если они не установлены, переустановите последнюю версию агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="1dd77-556">Убедитесь, что агент `omsconfig` может взаимодействовать со службой OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="1dd77-557">Выполните команду `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="1dd77-558">В результате выполнения этой команды возвращается конфигурация, полученная агентом с портала, в том числе параметры системного журнала, счетчики производительности Linux и пользовательские журналы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="1dd77-559">Если при выполнении команды выше произойдет сбой, выполните команду `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="1dd77-560">Эта команда позволяет активировать принудительное взаимодействие агента omsconfig со службой OMS для получения сведений о последней конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1dd77-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="1dd77-561">Пользовательские данные журнала Linux не отображаются на портале OMS</span><span class="sxs-lookup"><span data-stu-id="1dd77-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1dd77-562">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="1dd77-562">Probable causes</span></span>
* <span data-ttu-id="1dd77-563">Сбой при подключении к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="1dd77-564">Не установлен флажок **Apply the following configuration to my Linux Servers** (Применить следующую конфигурацию к моим серверам Linux).</span><span class="sxs-lookup"><span data-stu-id="1dd77-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="1dd77-565">Агент omsconfig не получил последний пользовательский журнал с портала.</span><span class="sxs-lookup"><span data-stu-id="1dd77-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="1dd77-566">Агенту `omsagent` не удалось получить доступ к пользовательскому журналу из-за отсутствующих разрешений или отсутствия `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="1dd77-567">В этом случае вы увидите следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="1dd77-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="1dd77-568">Это известная проблема с состоянием гонки, исправленная в агенте OMS для Linux версии 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="1dd77-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1dd77-569">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="1dd77-569">Resolutions</span></span>
* <span data-ttu-id="1dd77-570">Проверьте подключение (должен быть создан файл `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`).</span><span class="sxs-lookup"><span data-stu-id="1dd77-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="1dd77-571">При необходимости повторно установите подключение, используя командную строку omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="1dd77-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="1dd77-572">Дополнительные сведения см. в разделе [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Подключение с помощью командной строки).</span><span class="sxs-lookup"><span data-stu-id="1dd77-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="1dd77-573">На портале OMS в разделе **Параметры** на вкладке **Данные** установите флажок **Apply the following configuration to my Linux Servers** (Применить следующую конфигурацию к моим серверам Linux).</span><span class="sxs-lookup"><span data-stu-id="1dd77-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="1dd77-574">![Применить конфигурацию](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="1dd77-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="1dd77-575">Убедитесь, что агент `omsconfig` может взаимодействовать со службой OMS.</span><span class="sxs-lookup"><span data-stu-id="1dd77-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="1dd77-576">Выполните команду `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="1dd77-577">В результате выполнения этой команды возвращается конфигурация, полученная агентом с портала, в том числе параметры системного журнала, счетчики производительности Linux и пользовательские журналы.</span><span class="sxs-lookup"><span data-stu-id="1dd77-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="1dd77-578">Если при выполнении команды выше произойдет сбой, выполните команду `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="1dd77-579">Эта команда позволяет активировать принудительное взаимодействие агента omsconfig со службой OMS для получения сведений о последней конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1dd77-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="1dd77-580">Вместо привилегированного пользователя `root`, агент OMS для Linux выполняется от имени пользователя `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="1dd77-581">В большинстве случаев для чтения определенных файлов пользователю необходимо предоставить явное разрешение.</span><span class="sxs-lookup"><span data-stu-id="1dd77-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="1dd77-582">Чтобы предоставить разрешения пользователю `omsagent`, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1dd77-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="1dd77-583">Добавьте пользователя `omsagent` в определенную группу с помощью команды `sudo usermod -a -G <GROUPNAME> <USERNAME>`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="1dd77-584">Предоставьте универсальный доступ на чтение для требуемого файла с помощью команды `sudo chmod -R ugo+rw <FILE DIRECTORY>`.</span><span class="sxs-lookup"><span data-stu-id="1dd77-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="1dd77-585">Это известная проблема с состоянием гонки, исправленная в агенте OMS для Linux версии 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="1dd77-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="1dd77-586">После обновления агента до последней версии выполните следующую команду, чтобы получить последнюю версию подключаемого модуля выходных данных.</span><span class="sxs-lookup"><span data-stu-id="1dd77-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="1dd77-587">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="1dd77-587">Known limitations</span></span>
<span data-ttu-id="1dd77-588">Ознакомьтесь со следующими разделами, чтобы узнать о текущих ограничениях агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd77-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="1dd77-589">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="1dd77-589">Azure Diagnostics</span></span>
<span data-ttu-id="1dd77-590">Для виртуальных машин Linux в Azure может потребоваться выполнить дополнительные действия, чтобы разрешить сбор данных с помощью системы диагностики Azure и Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="1dd77-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="1dd77-591">**версии 2.2** .</span><span class="sxs-lookup"><span data-stu-id="1dd77-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="1dd77-592">Дополнительные сведения об установке и настройке расширения диагностики для Linux см. в разделе [Включение диагностического расширения Linux с помощью команды Azure CLI](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="1dd77-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="1dd77-593">**Обновление расширения диагностики с версии 2.0 до версии 2.2 ASM интерфейса командной строки Azure:**</span><span class="sxs-lookup"><span data-stu-id="1dd77-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="1dd77-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="1dd77-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="1dd77-595">В этих примерах команд указан файл PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="1dd77-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="1dd77-596">Этот файл должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1dd77-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="1dd77-597">sysklog не поддерживается</span><span class="sxs-lookup"><span data-stu-id="1dd77-597">Sysklog is not supported</span></span>
<span data-ttu-id="1dd77-598">Для сбора сообщений системного журнала требуется rsyslog или syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="1dd77-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="1dd77-599">Управляющая программа syslog по умолчанию не поддерживается для сбора событий системного журнала в Red Hat Enterprise Linux версии 5, CentOS и Oracle Linux (sysklog).</span><span class="sxs-lookup"><span data-stu-id="1dd77-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="1dd77-600">Чтобы собирать данные системного журнала из дистрибутивов этих версий, требуется установить и настроить управляющую программу rsyslog, которая заменит sysklog.</span><span class="sxs-lookup"><span data-stu-id="1dd77-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="1dd77-601">Дополнительные сведения о замене sysklog на rsyslog см. в разделе [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM) (Установка созданного RPM rsyslog).</span><span class="sxs-lookup"><span data-stu-id="1dd77-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd77-602">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1dd77-602">Next Steps</span></span>
* <span data-ttu-id="1dd77-603">[добавьте решения Log Analytics из коллекции решений](log-analytics-add-solutions.md) .</span><span class="sxs-lookup"><span data-stu-id="1dd77-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="1dd77-604">Подробные сведения, которые собирают решения, описаны в статье [про поиск по журналам](log-analytics-log-searches.md) .</span><span class="sxs-lookup"><span data-stu-id="1dd77-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="1dd77-605">Используйте [панели мониторинга](log-analytics-dashboards.md) для сохранения и отображения настраиваемых систем поиска.</span><span class="sxs-lookup"><span data-stu-id="1dd77-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
