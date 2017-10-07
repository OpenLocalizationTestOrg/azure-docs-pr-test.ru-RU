---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="384ff-101">Подключение к tooLog компьютеров Linux аналитика</span><span class="sxs-lookup"><span data-stu-id="384ff-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="384ff-102">Log Analytics позволяет собирать и обрабатывать данные, созданные компьютерами Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="384ff-103">Добавление данных, собранных из Linux tooOMS позволяет toomanage системами и контейнерными решениями, такими как Docker, независимо от того, где находятся компьютеры, — практически везде.</span><span class="sxs-lookup"><span data-stu-id="384ff-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="384ff-104">Источники данных могут находятся в центре обработки данных в локальной как физические серверы, виртуальные компьютеры в службе, размещенной в облаке, например Amazon Web Services (AWS) или Microsoft Azure, или даже hello портативный компьютер в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="384ff-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="384ff-105">Кроме того, OMS аналогичным образом собирает данные с компьютеров Windows. Так что это решение поддерживает гибридную ИТ-среду.</span><span class="sxs-lookup"><span data-stu-id="384ff-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="384ff-106">С помощью Log Analytics в OMS можно просматривать данные из всех этих источников и управлять ими на едином портале управления.</span><span class="sxs-lookup"><span data-stu-id="384ff-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="384ff-107">Это уменьшает необходимость hello toomonitor его с помощью различных систем, позволяет легко tooconsume и позволяет экспортировать любые данные, например toowhatever бизнес-аналитика решения или системы, у вас уже есть.</span><span class="sxs-lookup"><span data-stu-id="384ff-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="384ff-108">Эта статья содержит краткое руководство, которое поможет сбора и управления данными для компьютеров Linux с помощью hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="384ff-109">Дополнительные технические сведения, такие как конфигурация прокси-сервера, сведения о метриках CollectD и пользовательских источниках данных JSON, см. в [обзоре агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) и [полной документации по агенту OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="384ff-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="384ff-110">В настоящее время можно собирать следующие типы данных с компьютеров Linux hello:</span><span class="sxs-lookup"><span data-stu-id="384ff-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="384ff-111">Метрики производительности</span><span class="sxs-lookup"><span data-stu-id="384ff-111">Performance metrics</span></span>
* <span data-ttu-id="384ff-112">события системного журнала;</span><span class="sxs-lookup"><span data-stu-id="384ff-112">Syslog events</span></span>
* <span data-ttu-id="384ff-113">оповещения Nagios и Zabbix;</span><span class="sxs-lookup"><span data-stu-id="384ff-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="384ff-114">метрики производительности, данные инвентаризации и журналов контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="384ff-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="384ff-115">Поддерживаемые версии Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-115">Supported Linux versions</span></span>
<span data-ttu-id="384ff-116">x86 и x64 являются официально поддерживаемыми версиями в различных дистрибутивах Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="384ff-117">Однако hello агента OMS для Linux также можно запустить на других дистрибутивах, которых нет в списке.</span><span class="sxs-lookup"><span data-stu-id="384ff-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="384ff-118">выпуски Amazon Linux 2012.09–2015.09;</span><span class="sxs-lookup"><span data-stu-id="384ff-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="384ff-119">CentOS Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="384ff-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="384ff-120">Oracle Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="384ff-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="384ff-121">сервер Red Hat Enterprise Linux 5, 6 и 7;</span><span class="sxs-lookup"><span data-stu-id="384ff-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="384ff-122">Debian GNU/Linux 6, 7 и 8;</span><span class="sxs-lookup"><span data-stu-id="384ff-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="384ff-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10;</span><span class="sxs-lookup"><span data-stu-id="384ff-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="384ff-124">SUSE Linux Enterprise Server 11 и 12.</span><span class="sxs-lookup"><span data-stu-id="384ff-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="384ff-125">Агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-125">OMS Agent for Linux</span></span>
<span data-ttu-id="384ff-126">Hello агент Operations Management Suite для Linux состоит из нескольких пакетов.</span><span class="sxs-lookup"><span data-stu-id="384ff-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="384ff-127">Hello файл версии содержит следующие пакеты, работающей hello оболочку пакета с hello `--extract`.</span><span class="sxs-lookup"><span data-stu-id="384ff-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="384ff-128">**Package**</span><span class="sxs-lookup"><span data-stu-id="384ff-128">**Package**</span></span> | <span data-ttu-id="384ff-129">**Версия**</span><span class="sxs-lookup"><span data-stu-id="384ff-129">**Version**</span></span> | <span data-ttu-id="384ff-130">**Описание**</span><span class="sxs-lookup"><span data-stu-id="384ff-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="384ff-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="384ff-131">omsagent</span></span> |<span data-ttu-id="384ff-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="384ff-132">1.1.0</span></span> |<span data-ttu-id="384ff-133">Hello агент Operations Management Suite для Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="384ff-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="384ff-134">omsconfig</span></span> |<span data-ttu-id="384ff-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="384ff-135">1.1.1</span></span> |<span data-ttu-id="384ff-136">Агент конфигурации для агента OMS hello</span><span class="sxs-lookup"><span data-stu-id="384ff-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="384ff-137">omi</span><span class="sxs-lookup"><span data-stu-id="384ff-137">omi</span></span> |<span data-ttu-id="384ff-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="384ff-138">1.0.8.3</span></span> |<span data-ttu-id="384ff-139">OMI (Open Management Infrastructure) — упрощенная версия сервера CIM</span><span class="sxs-lookup"><span data-stu-id="384ff-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="384ff-140">scx</span><span class="sxs-lookup"><span data-stu-id="384ff-140">scx</span></span> |<span data-ttu-id="384ff-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="384ff-141">1.6.2</span></span> |<span data-ttu-id="384ff-142">Поставщики OMI CIM для метрик производительности операционной системы</span><span class="sxs-lookup"><span data-stu-id="384ff-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="384ff-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="384ff-143">apache-cimprov</span></span> |<span data-ttu-id="384ff-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="384ff-144">1.0.0</span></span> |<span data-ttu-id="384ff-145">Поставщик мониторинга производительности сервера Apache HTTP Server для OMI.</span><span class="sxs-lookup"><span data-stu-id="384ff-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="384ff-146">Устанавливается только при обнаружении сервера Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="384ff-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="384ff-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="384ff-147">mysql-cimprov</span></span> |<span data-ttu-id="384ff-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="384ff-148">1.0.0</span></span> |<span data-ttu-id="384ff-149">Поставщик мониторинга производительности сервера MySQL для OMI.</span><span class="sxs-lookup"><span data-stu-id="384ff-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="384ff-150">Устанавливается только при обнаружении сервера MySQL или MariaDB</span><span class="sxs-lookup"><span data-stu-id="384ff-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="384ff-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="384ff-151">docker-cimprov</span></span> |<span data-ttu-id="384ff-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="384ff-152">0.1.0</span></span> |<span data-ttu-id="384ff-153">Поставщик Docker для OMI.</span><span class="sxs-lookup"><span data-stu-id="384ff-153">Docker provider for OMI.</span></span> <span data-ttu-id="384ff-154">Устанавливается только при обнаружении Docker</span><span class="sxs-lookup"><span data-stu-id="384ff-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="384ff-155">Дополнительные артефакты установки</span><span class="sxs-lookup"><span data-stu-id="384ff-155">Additional installation artifacts</span></span>
<span data-ttu-id="384ff-156">После установки агента OMS hello для пакетов Linux, hello следующие дополнительные системные применяются изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="384ff-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="384ff-157">Эти артефакты удаляются при удалении пакета omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="384ff-158">Создается непривилегированный пользователь с именем `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="384ff-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="384ff-159">Это hello hello omsagent управляющая программа выполняется как</span><span class="sxs-lookup"><span data-stu-id="384ff-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="384ff-160">Создается файл «include» sudoers в /etc/sudoers.d/omsagent это разрешает omsagent toorestart hello syslog и omsagent управляющие программы.</span><span class="sxs-lookup"><span data-stu-id="384ff-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="384ff-161">Если директивы «include» sudo не поддерживаются в версии hello установки sudo, эти операции будут записаны слишком/д/sudoers.</span><span class="sxs-lookup"><span data-stu-id="384ff-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="384ff-162">Конфигурация syslog Hello — измененные tooforward подмножество событий toohello агента.</span><span class="sxs-lookup"><span data-stu-id="384ff-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="384ff-163">Дополнительные сведения см. в разделе hello **Настройка сбора данных** ниже</span><span class="sxs-lookup"><span data-stu-id="384ff-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="384ff-164">Сведения о сборе данных Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-164">Linux data collection details</span></span>
<span data-ttu-id="384ff-165">Hello следующей таблице приведены методы сбора данных и другие сведения о сборе данных.</span><span class="sxs-lookup"><span data-stu-id="384ff-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="384ff-166">источник</span><span class="sxs-lookup"><span data-stu-id="384ff-166">source</span></span> | <span data-ttu-id="384ff-167">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="384ff-167">Direct Agent</span></span> | <span data-ttu-id="384ff-168">Агент SCOM</span><span class="sxs-lookup"><span data-stu-id="384ff-168">SCOM agent</span></span> | <span data-ttu-id="384ff-169">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="384ff-169">Azure Storage</span></span> | <span data-ttu-id="384ff-170">Нужен ли SCOM?</span><span class="sxs-lookup"><span data-stu-id="384ff-170">SCOM required?</span></span> | <span data-ttu-id="384ff-171">Отправка данных агента SCOM через группу управления</span><span class="sxs-lookup"><span data-stu-id="384ff-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="384ff-172">Частота сбора</span><span class="sxs-lookup"><span data-stu-id="384ff-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="384ff-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="384ff-173">Zabbix</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="384ff-179">1 минута</span><span class="sxs-lookup"><span data-stu-id="384ff-179">1 minute</span></span> |
| <span data-ttu-id="384ff-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="384ff-180">Nagios</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="384ff-186">При получении</span><span class="sxs-lookup"><span data-stu-id="384ff-186">on arrival</span></span> |
| <span data-ttu-id="384ff-187">syslog</span><span class="sxs-lookup"><span data-stu-id="384ff-187">syslog</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="384ff-193">Из хранилища Azure — 10 минут, из агента — при получении</span><span class="sxs-lookup"><span data-stu-id="384ff-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="384ff-194">Счетчики производительности Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-194">Linux performance counters</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="384ff-200">По расписанию, не менее 10 секунд</span><span class="sxs-lookup"><span data-stu-id="384ff-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="384ff-201">Отслеживание изменений</span><span class="sxs-lookup"><span data-stu-id="384ff-201">change tracking</span></span> |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="384ff-207">Ежечасно</span><span class="sxs-lookup"><span data-stu-id="384ff-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="384ff-208">Требования к пакетам</span><span class="sxs-lookup"><span data-stu-id="384ff-208">Package Requirements</span></span>
| <span data-ttu-id="384ff-209">**Требуемый пакет**</span><span class="sxs-lookup"><span data-stu-id="384ff-209">**Required package**</span></span> | <span data-ttu-id="384ff-210">**Описание**</span><span class="sxs-lookup"><span data-stu-id="384ff-210">**Description**</span></span> | <span data-ttu-id="384ff-211">**Минимальная версия**</span><span class="sxs-lookup"><span data-stu-id="384ff-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="384ff-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="384ff-212">Glibc</span></span> |<span data-ttu-id="384ff-213">Библиотека C GNU</span><span class="sxs-lookup"><span data-stu-id="384ff-213">GNU C library</span></span> |<span data-ttu-id="384ff-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="384ff-214">2.5-12</span></span> |
| <span data-ttu-id="384ff-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="384ff-215">Openssl</span></span> |<span data-ttu-id="384ff-216">Библиотеки OpenSSL</span><span class="sxs-lookup"><span data-stu-id="384ff-216">OpenSSL libraries</span></span> |<span data-ttu-id="384ff-217">0.9.8e или 1.0</span><span class="sxs-lookup"><span data-stu-id="384ff-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="384ff-218">Curl</span><span class="sxs-lookup"><span data-stu-id="384ff-218">Curl</span></span> |<span data-ttu-id="384ff-219">Веб-клиент cURL</span><span class="sxs-lookup"><span data-stu-id="384ff-219">cURL web client</span></span> |<span data-ttu-id="384ff-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="384ff-220">7.15.5</span></span> |
| <span data-ttu-id="384ff-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="384ff-221">Python-ctypes</span></span> |<span data-ttu-id="384ff-222">Библиотеки функций</span><span class="sxs-lookup"><span data-stu-id="384ff-222">function libraries</span></span> |<span data-ttu-id="384ff-223">Недоступно</span><span class="sxs-lookup"><span data-stu-id="384ff-223">n/a</span></span> |
| <span data-ttu-id="384ff-224">PAM</span><span class="sxs-lookup"><span data-stu-id="384ff-224">PAM</span></span> |<span data-ttu-id="384ff-225">Подключаемые модули аутентификации</span><span class="sxs-lookup"><span data-stu-id="384ff-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="384ff-226">Недоступно</span><span class="sxs-lookup"><span data-stu-id="384ff-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="384ff-227">Rsyslog или syslog-ng, требуется toocollect syslog-сообщения.</span><span class="sxs-lookup"><span data-stu-id="384ff-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="384ff-228">управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog.</span><span class="sxs-lookup"><span data-stu-id="384ff-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="384ff-229">toocollect данных syslog из этой версии данных дистрибутивов hello rsyslog управляющая программа должна быть установлена и настроена tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="384ff-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="384ff-230">Быстрая установка</span><span class="sxs-lookup"><span data-stu-id="384ff-230">Quick install</span></span>
<span data-ttu-id="384ff-231">Запустите следующие команды toodownload hello omsagent hello, проверки контрольной суммы hello, а затем Установка и встроенного hello агента.</span><span class="sxs-lookup"><span data-stu-id="384ff-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="384ff-232">Команды предназначены для 64-разрядных систем.</span><span class="sxs-lookup"><span data-stu-id="384ff-232">Commands are for 64-bit.</span></span> <span data-ttu-id="384ff-233">Hello идентификатор рабочей области и первичный ключ можно найти на портале OMS hello под **параметры** на hello **подключенные источники** вкладки.</span><span class="sxs-lookup"><span data-stu-id="384ff-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![сведения о рабочей области](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="384ff-235">Существует множество других методов tooinstall hello агента и его обновления.</span><span class="sxs-lookup"><span data-stu-id="384ff-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="384ff-236">Вы можете прочитать больше о них на [hello tooinstall действия агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="384ff-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="384ff-237">Вы также можете просмотреть hello [Azure видеоруководство](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="384ff-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="384ff-238">Выбор метода сбора данных Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="384ff-239">Выбор hello типов данных, которые бы как toocollect зависит от того, нужно ли портал OMS toouse hello, или если необходимо изменение различных конфигурационных файлов непосредственно на клиентах Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="384ff-240">При выборе toouse hello портала конфигурации hello автоматически отправляется tooall клиентские компьютеры Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="384ff-241">Если необходимы различные конфигурации для разных клиентов Linux будет необходима tooedit клиентских файлов по отдельности или использовать альтернативу, например PowerShell DSC, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="384ff-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="384ff-242">Можно указать события syslog hello и счетчики производительности, которые должны toocollect с помощью файлов конфигурации на компьютерах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="384ff-243">*Если выбрана tooconfigure сбора данных путем изменения файлов конфигурации агента, следует отключить централизованную конфигурацию hello.*</span><span class="sxs-lookup"><span data-stu-id="384ff-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="384ff-244">Инструкции приведены ниже tooconfigure сбора данных в агент hello файлы конфигурации, а также toodisable централизованной конфигурации для всех агентов OMS для Linux или отдельных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="384ff-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="384ff-245">Отключение управления OMS для отдельного компьютера Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="384ff-246">Централизованный сбор данных для данных конфигурации для отдельного компьютера Linux с помощью сценария OMS_MetaConfigHelper.py hello будет отключена.</span><span class="sxs-lookup"><span data-stu-id="384ff-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="384ff-247">Это может быть полезно, если подмножеству компьютеров требуется специальная конфигурация.</span><span class="sxs-lookup"><span data-stu-id="384ff-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="384ff-248">toodisable централизованной конфигурации:</span><span class="sxs-lookup"><span data-stu-id="384ff-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="384ff-249">toore Включение централизованной конфигурации:</span><span class="sxs-lookup"><span data-stu-id="384ff-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="384ff-250">Счетчики производительности Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-250">Linux performance counters</span></span>
<span data-ttu-id="384ff-251">Счетчики производительности Linux, похожие счетчики производительности tooWindows — оба работают одинаково.</span><span class="sxs-lookup"><span data-stu-id="384ff-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="384ff-252">Можно использовать следующие процедуры tooadd hello и их настройки.</span><span class="sxs-lookup"><span data-stu-id="384ff-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="384ff-253">После добавления tooOMS, данные собираются для них каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="384ff-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="384ff-254">tooadd счетчика производительности Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="384ff-255">tooconfigure агенты OMS для Linux с помощью портала OMS hello, добавьте счетчики производительности Linux на странице "Параметры" hello щелкните **данные**.</span><span class="sxs-lookup"><span data-stu-id="384ff-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="384ff-256">На hello **параметры** в разделе **данные** , нажмите кнопку **счетчики производительности Linux** и затем выберите или введите имя hello hello счетчика требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="384ff-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="384ff-257">![Данные](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="384ff-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="384ff-258">Если вы не знаете полное имя счетчика hello hello, можно начать вводить часть имени, и появится список доступных счетчиков.</span><span class="sxs-lookup"><span data-stu-id="384ff-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="384ff-259">Когда счетчик hello вы tooadd, выберите имя hello hello списка и нажмите кнопку hello, а также значок tooadd hello счетчика.</span><span class="sxs-lookup"><span data-stu-id="384ff-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="384ff-260">После добавления счетчиков hello, он отображается в списке hello счетчиков и будет выделен цветной линией.</span><span class="sxs-lookup"><span data-stu-id="384ff-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="384ff-261">По умолчанию hello **применить указанную ниже конфигурацию toomy машины** выбран параметр.</span><span class="sxs-lookup"><span data-stu-id="384ff-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="384ff-262">Toodisable отправку данных конфигурации, снимите выделение hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="384ff-263">Закончив изменение счетчиков производительности, hello нижней части страницы приветствия щелкните **Сохранить** toofinalize изменения.</span><span class="sxs-lookup"><span data-stu-id="384ff-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="384ff-264">изменения конфигурации Hello внесенные отправляются hello tooall агенты OMS для Linux, которые зарегистрированы в OMS, обычно это занимает 5 минут.</span><span class="sxs-lookup"><span data-stu-id="384ff-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="384ff-265">Настройка счетчиков производительности Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="384ff-266">Для каждого счетчика производительности Windows можно выбрать конкретный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="384ff-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="384ff-267">Однако любой экземпляр счетчика, выбранный для счетчиков производительности Linux, применяется tooall дочерним счетчикам родительского счетчика hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="384ff-268">Hello следующей таблице показаны распространенные экземпляров hello tooboth доступные счетчики производительности Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="384ff-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="384ff-269">**Имя экземпляра**</span><span class="sxs-lookup"><span data-stu-id="384ff-269">**Instance name**</span></span> | <span data-ttu-id="384ff-270">**Значение**</span><span class="sxs-lookup"><span data-stu-id="384ff-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="384ff-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="384ff-271">\_Total</span></span> |<span data-ttu-id="384ff-272">Общее количество всех экземпляров hello</span><span class="sxs-lookup"><span data-stu-id="384ff-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="384ff-273">Все экземпляры</span><span class="sxs-lookup"><span data-stu-id="384ff-273">All instances</span></span> |
| <span data-ttu-id="384ff-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="384ff-274">(/&#124;/var)</span></span> |<span data-ttu-id="384ff-275">Сопоставление экземпляров с именем / или/var</span><span class="sxs-lookup"><span data-stu-id="384ff-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="384ff-276">Аналогичным образом hello интервал выборки, выбранный для родительского счетчика, применяется tooall его дочерним счетчикам.</span><span class="sxs-lookup"><span data-stu-id="384ff-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="384ff-277">Другими словами интервалы выборки счетчика дочерних hello и экземпляры всех связаны друг с другом.</span><span class="sxs-lookup"><span data-stu-id="384ff-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="384ff-278">Добавление и настройка метрик производительности в Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="384ff-279">Toocollect метрики производительности определяются hello конфигурации в каталоге/и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="384ff-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="384ff-280">В разделе [доступные метрики производительности](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) доступные классы и метрики для агента OMS для Linux hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="384ff-281">Каждый объект или категория toocollect метрик производительности должен быть определен в файле конфигурации hello как один `<source>` элемента.</span><span class="sxs-lookup"><span data-stu-id="384ff-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="384ff-282">следующий синтаксис Hello hello шаблону ниже.</span><span class="sxs-lookup"><span data-stu-id="384ff-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="384ff-283">используются следующие настраиваемые параметры Hello этого элемента:</span><span class="sxs-lookup"><span data-stu-id="384ff-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="384ff-284">**Объект\_имя**: hello имя объекта для коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="384ff-285">**Экземпляр\_regex**: *регулярное выражение* определение какие toocollect экземпляров.</span><span class="sxs-lookup"><span data-stu-id="384ff-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="384ff-286">Здравствуйте, значение: `.*` указывает все экземпляры.</span><span class="sxs-lookup"><span data-stu-id="384ff-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="384ff-287">toocollect метрик процессора только hello \_общий экземпляр можно указать `_Total`.</span><span class="sxs-lookup"><span data-stu-id="384ff-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="384ff-288">только toocollect метрик процесса для hello экземпляров crond или sshd, можно указать: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="384ff-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="384ff-289">**Счетчик\_имя\_regex**: *регулярное выражение* определение toocollect какие счетчики (hello объекта).</span><span class="sxs-lookup"><span data-stu-id="384ff-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="384ff-290">Укажите все счетчики объекта hello toocollect: `.*`.</span><span class="sxs-lookup"><span data-stu-id="384ff-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="384ff-291">toocollect только данные счетчиков пространства подкачки hello объекта памяти, можно указать:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="384ff-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="384ff-292">**Интервал:**: hello частоту, с которой hello собираются данные счетчиков объекта.</span><span class="sxs-lookup"><span data-stu-id="384ff-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="384ff-293">— Конфигурация по умолчанию Hello для метрики производительности:</span><span class="sxs-lookup"><span data-stu-id="384ff-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="384ff-294">Включение счетчиков производительности MySQL с помощью команд Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="384ff-295">Если сервер MySQL или MariaDB Server обнаруживается hello компьютера при установке пакета omsagent hello, поставщик для сервера MySQL наблюдения за производительностью автоматически устанавливается.</span><span class="sxs-lookup"><span data-stu-id="384ff-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="384ff-296">Этот поставщик подключается toohello локального MySQL или MariaDB tooexpose статистики производительности сервера.</span><span class="sxs-lookup"><span data-stu-id="384ff-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="384ff-297">Необходимо tooconfigure учетные данные пользователя MySQL hello поставщик можно получить доступ к MySQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="384ff-298">toodefine пользователя по умолчанию учетная запись для hello MySQL server в localhost, hello используйте следующий пример команды.</span><span class="sxs-lookup"><span data-stu-id="384ff-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="384ff-299">Hello учетных данных файл должен быть доступен для чтения для учетной записи omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="384ff-300">Выполнение hello выполнить команду mycimprovauth от имени omsgent рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="384ff-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="384ff-301">Кроме того, можно указать hello необходимые учетные данные MySQL в файле, создав файл hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Дополнительные сведения об управлении учетными данными MySQL для отслеживания с помощью файла mysql-auth hello см. в разделе [мониторинга учетные данные в файле проверки подлинности hello управление MySQL](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="384ff-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="384ff-302">В разделе [базы данных разрешения, необходимые для счетчиков производительности MySQL](#database-permissions-required-for-mysql-performance-counters) подробные сведения о разрешениях объекта, предусмотренного toocollect пользователя MySQL hello данных производительности MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="384ff-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="384ff-303">Включение счетчиков производительности сервера Apache HTTP Server с помощью команд Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="384ff-304">Если при установке пакета omsagent hello на компьютере hello обнаружен HTTP-сервера Apache, автоматически устанавливается поставщик для HTTP-сервера Apache наблюдения за производительностью.</span><span class="sxs-lookup"><span data-stu-id="384ff-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="384ff-305">Этот поставщик использует «модуль», должны быть загружены в hello HTTP-сервера Apache в данные производительности о заказах tooaccess Apache.</span><span class="sxs-lookup"><span data-stu-id="384ff-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="384ff-306">Можно загрузить модуль hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="384ff-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="384ff-307">toounload hello Apache модуль мониторинга, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="384ff-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="384ff-308">tooview данные о производительности с помощью аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="384ff-309">На портале Operations Management Suite hello щелкните плитку hello поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="384ff-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="384ff-310">Введите в строке поиска hello `* (Type=Perf)` tooview всех счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="384ff-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="384ff-311">Поскольку OMS также собирает данные счетчика производительности Windows, вы должны ограничить hello tooLinux данных поиска.</span><span class="sxs-lookup"><span data-stu-id="384ff-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="384ff-312">Таким образом hello примере будут отображаться производительности данных конкретного tooan сервера Linux с именем Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="384ff-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![пример сервера, отображающийся на странице результатов поиска](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="384ff-314">В результатах hello, можно щелкнуть **метрики** tooview hello счетчики, которые были собраны данные.</span><span class="sxs-lookup"><span data-stu-id="384ff-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="384ff-315">Данные в реальном времени отображаются в виде графиков для каждого счетчика.</span><span class="sxs-lookup"><span data-stu-id="384ff-315">Real-time data is shown as graphs for each counter.</span></span>

![Метрики](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="384ff-317">syslog</span><span class="sxs-lookup"><span data-stu-id="384ff-317">Syslog</span></span>
<span data-ttu-id="384ff-318">Syslog — это событие, ведение журнала протокола аналогичные tooWindows журналы событий — оба работают одинаково в OMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="384ff-319">tooadd нового средства syslog Linux в OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="384ff-320">На hello **параметры** в разделе **данные** , нажмите кнопку **Syslog** и toohello слева hello и значок, введите имя средства syslog hello, которое следует tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="384ff-321">![Системный журнал Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="384ff-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="384ff-322">Если вы не знаете полное имя hello hello подсистемы, можно начать вводить часть имени, и появится список доступных средств syslog.</span><span class="sxs-lookup"><span data-stu-id="384ff-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="384ff-323">При обнаружении hello средства syslog, что вы tooadd, выберите имя hello hello списка и нажмите кнопку hello, а также значок tooadd hello средства syslog.</span><span class="sxs-lookup"><span data-stu-id="384ff-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="384ff-324">После добавления hello услуги, он отображается в списке hello будет выделено цветной линией.</span><span class="sxs-lookup"><span data-stu-id="384ff-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="384ff-325">Затем выберите hello степени серьезности (категорий сведений средства syslog), которые должны toocollect.</span><span class="sxs-lookup"><span data-stu-id="384ff-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="384ff-326">Hello нижней части страницы приветствия щелкните **Сохранить** toofinalize изменения.</span><span class="sxs-lookup"><span data-stu-id="384ff-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="384ff-327">изменения конфигурации Hello внесенные отправляются hello tooall агенты OMS для Linux, которые зарегистрированы в OMS, обычно это занимает 5 минут.</span><span class="sxs-lookup"><span data-stu-id="384ff-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="384ff-328">Настройка устройств системного журнала Linux в Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="384ff-329">События syslog отправляются из управляющей программы syslog hello, например rsyslog или syslog-ng, tooa локальный порт, агентом Здравствуй прослушивает.</span><span class="sxs-lookup"><span data-stu-id="384ff-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="384ff-330">Порт по умолчанию — 25224.</span><span class="sxs-lookup"><span data-stu-id="384ff-330">By default, port 25224.</span></span> <span data-ttu-id="384ff-331">При установке агента hello, применяется конфигурация syslog по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="384ff-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="384ff-332">Ее можно найти в следующих каталогах:</span><span class="sxs-lookup"><span data-stu-id="384ff-332">This is found at:</span></span>

<span data-ttu-id="384ff-333">rsyslog — /etc/rsyslog.d/rsyslog-oms.conf;</span><span class="sxs-lookup"><span data-stu-id="384ff-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="384ff-334">syslog-ng — /etc/syslog-ng/syslog-ng.conf.</span><span class="sxs-lookup"><span data-stu-id="384ff-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="384ff-335">по умолчанию Hello: Конфигурация syslog агента OMS передает события syslog из всех средств с уровнем серьезности «предупреждение» или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="384ff-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="384ff-336">При изменении конфигурации syslog hello, необходимо перезапустить управляющая программа syslog hello для эффекта tootake изменения hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="384ff-337">Hello конфигурация syslog по умолчанию для hello агента OMS для Linux для OMS является:</span><span class="sxs-lookup"><span data-stu-id="384ff-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="384ff-338">При использовании rsyslog:</span><span class="sxs-lookup"><span data-stu-id="384ff-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="384ff-339">При использовании syslog-ng:</span><span class="sxs-lookup"><span data-stu-id="384ff-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="384ff-340">tooview все события системного журнала с помощью аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="384ff-341">На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.</span><span class="sxs-lookup"><span data-stu-id="384ff-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="384ff-342">В hello **управление журналом** группирование, выберите поиска стандартных системного журнала, а затем выберите один toorun его.</span><span class="sxs-lookup"><span data-stu-id="384ff-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="384ff-343">В этом примере представлены все события системного журнала.</span><span class="sxs-lookup"><span data-stu-id="384ff-343">This example shows all Syslog events.</span></span>

![события системного журнала, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="384ff-345">Теперь вы можете подробно рассмотреть результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="384ff-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="384ff-346">Оповещения Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-346">Linux alerts</span></span>
<span data-ttu-id="384ff-347">При использовании Nagios или Zabbix toomanage компьютеры Linux, то OMS может получать hello предупреждения, созданные с помощью этих средств.</span><span class="sxs-lookup"><span data-stu-id="384ff-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="384ff-348">Тем не менее — в настоящее время нет метода tooconfigure входящих данных предупреждений с помощью портала OMS hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="384ff-349">Вместо этого необходим tooedit конфигурации файла toostart отправку оповещений tooOMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="384ff-350">Сбор оповещений из Nagios</span><span class="sxs-lookup"><span data-stu-id="384ff-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="384ff-351">toocollect предупреждения с сервера Nagios, необходимо toomake hello после изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="384ff-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="384ff-352">Предоставление пользовательских hello **omsagent** toohello доступ на чтение для файла журнала Nagios (т. е. /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="384ff-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="384ff-353">При условии, что файл nagios.log hello принадлежит группе hello **nagios** , можно добавить пользователя hello **omsagent** toohello **nagios** группы.</span><span class="sxs-lookup"><span data-stu-id="384ff-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="384ff-354">Измените файл omsagent.confconfiguration hello (/ и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="384ff-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="384ff-355">Убедитесь, что присутствуют и не закомментированы следующие записи hello:</span><span class="sxs-lookup"><span data-stu-id="384ff-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="384ff-356">Перезапустите управляющую программу omsagent hello:</span><span class="sxs-lookup"><span data-stu-id="384ff-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="384ff-357">Сбор оповещений из Zabbix</span><span class="sxs-lookup"><span data-stu-id="384ff-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="384ff-358">toocollect предупреждений с сервера Zabbix выполните toothose аналогичные шаги для Nagios выше, за исключением того, потребуется toospecify пользователя и пароль в *открытый текст*.</span><span class="sxs-lookup"><span data-stu-id="384ff-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="384ff-359">Это не очень удобно, но в скором времени это требование может измениться.</span><span class="sxs-lookup"><span data-stu-id="384ff-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="384ff-360">tooaddress эту проблему, рекомендуется создать пользователя hello и предоставить ему разрешение toomonitor только.</span><span class="sxs-lookup"><span data-stu-id="384ff-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="384ff-361">Раздел примера файла конфигурации omsagent.conf hello (/ и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf) для Zabbix должен выглядеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="384ff-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="384ff-362">Просмотр оповещений с использованием поиска Log Analytics</span><span class="sxs-lookup"><span data-stu-id="384ff-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="384ff-363">После настройки вашей tooOMS оповещения toosend компьютеров Linux, можно использовать несколько простых поиска запросов tooview hello предупреждения журнала.</span><span class="sxs-lookup"><span data-stu-id="384ff-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="384ff-364">Hello следующем примере запрос поиска возвращает все записанные hello оповещения, которые были созданы.</span><span class="sxs-lookup"><span data-stu-id="384ff-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="384ff-365">Например если в ИТ-инфраструктуре возникает какая-либо проблемы, затем результаты для hello в следующем примере, что запрос может указывать на источник проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="384ff-366">Кроме того, вы можете легко просмотреть toohello оповещения по исходной системе toohelp узких расследования.</span><span class="sxs-lookup"><span data-stu-id="384ff-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="384ff-367">Hello преимущество заключается в отсутствии обязательно систем управления toovarious toogo от начала hello — при условии, что оповещения отправляются tooOMS, можно начать прямо отсюда.</span><span class="sxs-lookup"><span data-stu-id="384ff-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="384ff-368">tooview Nagios все оповещения с помощью аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="384ff-369">На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.</span><span class="sxs-lookup"><span data-stu-id="384ff-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="384ff-370">В строке запроса hello введите следующий запрос поиска hello</span><span class="sxs-lookup"><span data-stu-id="384ff-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![оповещения Nagios, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="384ff-372">После появления результатов поиска hello, можно просмотреть дополнительные сведения о таких как *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="384ff-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="384ff-373">tooview всех оповещений Zabbix с помощью аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="384ff-374">На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.</span><span class="sxs-lookup"><span data-stu-id="384ff-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="384ff-375">В строке запроса hello введите следующий запрос поиска hello</span><span class="sxs-lookup"><span data-stu-id="384ff-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![оповещения Zabbix, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="384ff-377">После появления результатов поиска hello, можно просмотреть дополнительные сведения о таких как *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="384ff-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="384ff-378">Совместимость с System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="384ff-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="384ff-379">Hello агента OMS для Linux использует двоичные файлы агента совместно с System Center Operations Manager агент hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="384ff-380">Установка hello агента OMS для Linux в системе под управлением Operations Manager обновления hello пакеты OMI и SCX на hello компьютера tooa новой версии.</span><span class="sxs-lookup"><span data-stu-id="384ff-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="384ff-381">Hello агента OMS для Linux и System Center 2012 R2 являются совместимыми.</span><span class="sxs-lookup"><span data-stu-id="384ff-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="384ff-382">Однако **System Center 2012 SP1 и более ранних версий не в настоящее время несовместимы или не поддерживаются с hello агента OMS для Linux.**</span><span class="sxs-lookup"><span data-stu-id="384ff-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="384ff-383">Если hello агента OMS для Linux — установленных tooa компьютера, который в настоящее время не находится под управлением Operations Manager и более поздней версии требуется компьютер hello toomanage с Operations Manager, необходимо изменить конфигурацию OMI hello перед обнаружением компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="384ff-384">**Этот шаг не требуется, если до hello агента OMS для Linux установлен агент Operations Manager hello.**</span><span class="sxs-lookup"><span data-stu-id="384ff-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="384ff-385">hello tooenable агента OMS для Linux toocommunicate с Operations Manager</span><span class="sxs-lookup"><span data-stu-id="384ff-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="384ff-386">Изменение файла /etc/opt/omi/conf/omiserver.conf hello</span><span class="sxs-lookup"><span data-stu-id="384ff-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="384ff-387">Убедитесь, что hello строки, начинающиеся с **httpsport =** hello порт 1270.</span><span class="sxs-lookup"><span data-stu-id="384ff-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="384ff-388">Таким образом — `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="384ff-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="384ff-389">Перезапустите сервер OMI hello:</span><span class="sxs-lookup"><span data-stu-id="384ff-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="384ff-390">Разрешения базы данных, необходимые для счетчиков производительности MySQL</span><span class="sxs-lookup"><span data-stu-id="384ff-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="384ff-391">toogrant разрешения tooa пользователя MySQL, hello пользователю необходимо иметь hello привилегию «предоставление», а также hello предоставляемое право.</span><span class="sxs-lookup"><span data-stu-id="384ff-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="384ff-392">Чтобы пользователь MySQL hello tooreturn производительности данных hello пользователь должен иметь доступа toohello следующие запросы:</span><span class="sxs-lookup"><span data-stu-id="384ff-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="384ff-393">В дополнение к этому toothese запросы hello MySQL пользователю требуется доступ SELECT toohello следующие таблицы по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="384ff-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="384ff-394">information_schema;</span><span class="sxs-lookup"><span data-stu-id="384ff-394">information_schema</span></span>
* <span data-ttu-id="384ff-395">mysql</span><span class="sxs-lookup"><span data-stu-id="384ff-395">mysql</span></span>

<span data-ttu-id="384ff-396">Эти права можно предоставить, запустив hello следующих команд grant.</span><span class="sxs-lookup"><span data-stu-id="384ff-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="384ff-397">Управление учетными данными в файле проверки подлинности hello мониторинга MySQL</span><span class="sxs-lookup"><span data-stu-id="384ff-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="384ff-398">Hello следующие разделы помогут управлять учетными данными MySQL.</span><span class="sxs-lookup"><span data-stu-id="384ff-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="384ff-399">Настройка поставщика MySQL OMI hello</span><span class="sxs-lookup"><span data-stu-id="384ff-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="384ff-400">Hello поставщик MySQL OMI требуется предварительно настроенный пользователь MySQL и установленные клиентские библиотеки MySQL порядок сведений о производительности и работоспособности tooquery hello из экземпляра MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="384ff-401">Файл аутентификации OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="384ff-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="384ff-402">Поставщик MySQL OMI использует toodetermine файла проверки подлинности выполняет прослушивание экземпляр MySQL hello какие адреса привязки и порта, и что учетные данные toouse toogather метрики.</span><span class="sxs-lookup"><span data-stu-id="384ff-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="384ff-403">Во время установки hello MySQL OMI поставщика будет проверять файлы конфигурации my.cnf MySQL (расположения по умолчанию) для адреса привязки и порта и частично набор hello файл проверки подлинности MySQL OMI.</span><span class="sxs-lookup"><span data-stu-id="384ff-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="384ff-404">Отслеживание toocomplete экземпляра сервера MySQL добавьте предварительно созданный файл проверки подлинности MySQL OMI в правильный каталог hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="384ff-405">Формат файла аутентификации</span><span class="sxs-lookup"><span data-stu-id="384ff-405">Authentication file format</span></span>
<span data-ttu-id="384ff-406">Hello файл проверки подлинности MySQL OMI является текстовый файл, содержащий сведения о:</span><span class="sxs-lookup"><span data-stu-id="384ff-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="384ff-407">Порт</span><span class="sxs-lookup"><span data-stu-id="384ff-407">Port</span></span>
* <span data-ttu-id="384ff-408">адрес привязки;</span><span class="sxs-lookup"><span data-stu-id="384ff-408">Bind-Address</span></span>
* <span data-ttu-id="384ff-409">имя пользователя MySQL;</span><span class="sxs-lookup"><span data-stu-id="384ff-409">MySQL username</span></span>
* <span data-ttu-id="384ff-410">пароль в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="384ff-410">Base64 encoded password</span></span>

<span data-ttu-id="384ff-411">только Hello файл проверки подлинности MySQL OMI предоставляет права доступа для пользователей Linux toohello чтения и записи, который его создал.</span><span class="sxs-lookup"><span data-stu-id="384ff-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="384ff-412">Файл проверки подлинности MySQL OMI по умолчанию содержит экземпляр по умолчанию и номер порта в зависимости от того, какие сведения доступны и проанализированы из hello найден файл конфигурации MySQL.</span><span class="sxs-lookup"><span data-stu-id="384ff-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="384ff-413">экземпляр по умолчанию Hello означает toomake, управление несколькими экземплярами MySQL на одном узле Linux проще и обозначается экземпляром hello с портом 0.</span><span class="sxs-lookup"><span data-stu-id="384ff-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="384ff-414">Все добавленные экземпляры наследуют свойства от экземпляра по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="384ff-415">Например при добавлении экземпляра MySQL, прослушивает порт «3308», адрес привязки, имя пользователя и пароль в кодировке Base64 экземпляра по умолчанию hello достигается используется tootry и отслеживать экземпляр hello прослушивание на порту 3308.</span><span class="sxs-lookup"><span data-stu-id="384ff-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="384ff-416">Если hello экземпляр в порту 3308 привязан tooanother адрес и использует hello же имя пользователя MySQL и пары пароль только hello необходимо заново указать hello необходимые адреса привязки и hello другие свойства будут унаследованы.</span><span class="sxs-lookup"><span data-stu-id="384ff-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="384ff-417">Примеры файла проверки подлинности hello напоминать следующий hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="384ff-418">Экземпляр по умолчанию и экземпляр с портом 3308:</span><span class="sxs-lookup"><span data-stu-id="384ff-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="384ff-419">Экземпляр по умолчанию и экземпляр с портом 3308 и другим паролем в кодировке Base 64:</span><span class="sxs-lookup"><span data-stu-id="384ff-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="384ff-420">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="384ff-420">**Property**</span></span> | <span data-ttu-id="384ff-421">**Описание**</span><span class="sxs-lookup"><span data-stu-id="384ff-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="384ff-422">Порт</span><span class="sxs-lookup"><span data-stu-id="384ff-422">Port</span></span> |<span data-ttu-id="384ff-423">Порт представляет hello текущий порт hello выполняет прослушивание экземпляр MySQL.</span><span class="sxs-lookup"><span data-stu-id="384ff-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="384ff-424">Hello порт 0 означает, что для экземпляра по умолчанию используются следующие свойства hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="384ff-425">адрес привязки;</span><span class="sxs-lookup"><span data-stu-id="384ff-425">Bind-Address</span></span> |<span data-ttu-id="384ff-426">Hello адрес привязки — hello текущий адрес привязки MySQL.</span><span class="sxs-lookup"><span data-stu-id="384ff-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="384ff-427">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="384ff-427">username</span></span> |<span data-ttu-id="384ff-428">Это имя пользователя hello hello пользователя MySQL, который следует экземпляра сервера MySQL hello toomonitor toouse.</span><span class="sxs-lookup"><span data-stu-id="384ff-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="384ff-429">пароль в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="384ff-429">Base64 encoded Password</span></span> |<span data-ttu-id="384ff-430">Это пароль hello hello пользователя MySQL, закодированный в Base64.</span><span class="sxs-lookup"><span data-stu-id="384ff-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="384ff-431">Автоматическое обновление</span><span class="sxs-lookup"><span data-stu-id="384ff-431">AutoUpdate</span></span> |<span data-ttu-id="384ff-432">После обновления поставщик OMI MySQL hello поставщика hello повторить сканирование на наличие изменений в файле my.cnf hello и перезаписывает файл проверки подлинности OMI MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="384ff-433">Установите этот флаг tootrue или false в зависимости от необходимых обновлений toohello MySQL OMI файл проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="384ff-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="384ff-434">Расположение файла аутентификации</span><span class="sxs-lookup"><span data-stu-id="384ff-434">Authentication file location</span></span>
<span data-ttu-id="384ff-435">Hello файл проверки подлинности OMI MySQL должен находится в следующие расположения hello и имя «mysql-auth»:</span><span class="sxs-lookup"><span data-stu-id="384ff-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="384ff-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="384ff-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="384ff-437">файл Hello (и каталог проверки auth/omsagent) должен принадлежать пользователю omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="384ff-438">Журналы агента</span><span class="sxs-lookup"><span data-stu-id="384ff-438">Agent logs</span></span>
<span data-ttu-id="384ff-439">журналы Hello hello агента OMS для Linux находятся в:</span><span class="sxs-lookup"><span data-stu-id="384ff-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="384ff-440">/var/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="384ff-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="384ff-441">Hello журналы hello агента OMS для Linux для omsconfig (конфигурация агента) находятся в:</span><span class="sxs-lookup"><span data-stu-id="384ff-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="384ff-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="384ff-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="384ff-443">Журналы для компонентов OMI и SCX hello (которые предоставляют данные метрик производительности) находятся в следующем:</span><span class="sxs-lookup"><span data-stu-id="384ff-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="384ff-444">/var/opt/omi/log/ и /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="384ff-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="384ff-445">Устранение неполадок hello агента OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="384ff-446">Используйте следующие сведения toodiagnose hello и устранение общих проблем.</span><span class="sxs-lookup"><span data-stu-id="384ff-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="384ff-447">Если ни один из hello, устранение неполадок в этом разделе поможет также можно hello следующие ресурсы toohelp устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="384ff-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="384ff-448">Клиенты с поддержкой Premier могут обратиться в службу поддержки [здесь](https://premier.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="384ff-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="384ff-449">Клиентам с соглашений для поддержки Azure можно зарегистрироваться поддержки по поводу hello [портал Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="384ff-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="384ff-450">Можно [сообщить о проблеме в GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).</span><span class="sxs-lookup"><span data-stu-id="384ff-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="384ff-451">Форум, посвященный обратной связи идеи и отчет об ошибках toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="384ff-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="384ff-452">Важные расположения журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-452">Important log locations</span></span>
| <span data-ttu-id="384ff-453">Файл</span><span class="sxs-lookup"><span data-stu-id="384ff-453">File</span></span> | <span data-ttu-id="384ff-454">Путь</span><span class="sxs-lookup"><span data-stu-id="384ff-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="384ff-455">Файл журнала агента OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="384ff-456">Файл журнала конфигурации агента OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="384ff-457">Важные файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="384ff-457">Important configuration files</span></span>
| <span data-ttu-id="384ff-458">Категория</span><span class="sxs-lookup"><span data-stu-id="384ff-458">Catergory</span></span> | <span data-ttu-id="384ff-459">Расположение файла</span><span class="sxs-lookup"><span data-stu-id="384ff-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="384ff-460">syslog</span><span class="sxs-lookup"><span data-stu-id="384ff-460">Syslog</span></span> |<span data-ttu-id="384ff-461">`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` или `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="384ff-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="384ff-462">Данные производительности, Nagios, Zabbix, выходные данные OMS и общая конфигурация агента</span><span class="sxs-lookup"><span data-stu-id="384ff-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="384ff-463">Дополнительные конфигурации</span><span class="sxs-lookup"><span data-stu-id="384ff-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="384ff-464">Если конфигурация портала OMS включена, при редактировании файлы конфигурации счетчиков производительности и системных журналов переопределяются.</span><span class="sxs-lookup"><span data-stu-id="384ff-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="384ff-465">Вы можете отключить конфигурацию в hello портал OMS (для всех узлов) или для отдельных узлов, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="384ff-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="384ff-466">Включение ведения журнала отладки</span><span class="sxs-lookup"><span data-stu-id="384ff-466">Enable debug logging</span></span>
<span data-ttu-id="384ff-467">Отладка tooenable ведения журнала, можно использовать подключаемый модуль вывода OMS hello и подробный вывод.</span><span class="sxs-lookup"><span data-stu-id="384ff-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="384ff-468">Подключаемый модуль выходных данных OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-468">OMS output plugin</span></span>
<span data-ttu-id="384ff-469">FluentD позволяет hello подключаемого модуля toospecify уровни ведения журнала для различных журнала уровней для входов и выходов.</span><span class="sxs-lookup"><span data-stu-id="384ff-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="384ff-470">toospecify другая степень журнал для вывода OMS, изменение конфигурации агента общие hello в hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` файла.</span><span class="sxs-lookup"><span data-stu-id="384ff-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="384ff-471">Hello внизу hello файл конфигурации, измените hello `log_level` свойство из `info` слишком`debug`.</span><span class="sxs-lookup"><span data-stu-id="384ff-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="384ff-472">Ведение журнала отладки позволяет службой OMS, разделенных тип, число элементов данных и время, затраченное toosend toohello передачи toosee в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="384ff-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="384ff-473">*Пример включенного журнала отладки.*</span><span class="sxs-lookup"><span data-stu-id="384ff-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="384ff-474">Подробные выходные данные</span><span class="sxs-lookup"><span data-stu-id="384ff-474">Verbose output</span></span>
<span data-ttu-id="384ff-475">Вместо того чтобы использовать подключаемый модуль вывода OMS hello, можно также вывести элементов данных непосредственно слишком`stdout`, которое отображается в hello агента OMS для Linux файла журнала.</span><span class="sxs-lookup"><span data-stu-id="384ff-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="384ff-476">В файле конфигурации общего агента OMS hello в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, hello OMS вывода подключаемого модуля, добавив комментарий горизонтального `#` перед каждой строки.</span><span class="sxs-lookup"><span data-stu-id="384ff-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="384ff-477">Ниже Здравствуйте подключаемого модуля выходные данные, удалить комментарий hello в следующем разделе, удалив hello hello `#` символ в начале каждой строки hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="384ff-478">Перенаправленных сообщений системного журнала не отображаются в журнале hello</span><span class="sxs-lookup"><span data-stu-id="384ff-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-479">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-479">Probable causes</span></span>
* <span data-ttu-id="384ff-480">Hello применения toohello Linux сервер конфигурации не разрешает сбор средства отправки hello и/или уровня ведения журнала</span><span class="sxs-lookup"><span data-stu-id="384ff-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="384ff-481">Syslog не пересылается правильно toohello сервера Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="384ff-482">Hello количество сообщений, направляются в секунду слишком велики для базовой конфигурации hello агента OMS для Linux toohandle hello</span><span class="sxs-lookup"><span data-stu-id="384ff-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-483">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-483">Resolutions</span></span>
* <span data-ttu-id="384ff-484">Проверка конфигурации hello в hello портал OMS для системного журнала имеет все возможности hello и уровни журнала hello</span><span class="sxs-lookup"><span data-stu-id="384ff-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="384ff-485">**OMS Portal (Портал OMS) > Параметры > Данные > Системный журнал**.</span><span class="sxs-lookup"><span data-stu-id="384ff-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="384ff-486">Убедитесь, что собственный syslog, управляющие программы обмена сообщениями (`rsyslog`, `syslog-ng`), может tooreceive hello перенаправленных сообщений</span><span class="sxs-lookup"><span data-stu-id="384ff-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="384ff-487">Проверьте параметры брандмауэра на tooensure сервера системного журнала hello, что сообщений не блокируются</span><span class="sxs-lookup"><span data-stu-id="384ff-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="384ff-488">Имитации tooOMS сообщения системного журнала, с помощью hello `logger` команды — например:</span><span class="sxs-lookup"><span data-stu-id="384ff-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="384ff-489">Проблемы с подключением tooOMS при использовании прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="384ff-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-490">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-490">Probable causes</span></span>
* <span data-ttu-id="384ff-491">Hello прокси-сервера указан неверный при установке и настройке агента hello</span><span class="sxs-lookup"><span data-stu-id="384ff-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="384ff-492">конечные точки службы OMS Hello не whitelistested в центре обработки данных</span><span class="sxs-lookup"><span data-stu-id="384ff-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-493">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-493">Resolutions</span></span>
* <span data-ttu-id="384ff-494">Переустановите hello агента OMS для Linux, используя следующую команду с параметром hello hello `-v` включена.</span><span class="sxs-lookup"><span data-stu-id="384ff-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="384ff-495">Это позволяет подробные выходные данные агента hello подключение через прокси-сервера hello toohello службой OMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="384ff-496">Ознакомьтесь с документацией hello для OMS прокси-сервера в [Настройка hello агент для использования с прокси-сервера HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="384ff-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="384ff-497">Убедитесь, что hello следующих конечных точек службы OMS входят</span><span class="sxs-lookup"><span data-stu-id="384ff-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="384ff-498">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="384ff-498">Agent Resource</span></span> | <span data-ttu-id="384ff-499">порты;</span><span class="sxs-lookup"><span data-stu-id="384ff-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="384ff-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="384ff-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="384ff-501">Порт 443</span><span class="sxs-lookup"><span data-stu-id="384ff-501">Port 443</span></span> |
| <span data-ttu-id="384ff-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="384ff-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="384ff-503">Порт 443</span><span class="sxs-lookup"><span data-stu-id="384ff-503">Port 443</span></span> |
| <span data-ttu-id="384ff-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="384ff-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="384ff-505">Порт 443</span><span class="sxs-lookup"><span data-stu-id="384ff-505">Port 443</span></span> |
| <span data-ttu-id="384ff-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="384ff-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="384ff-507">Порт 443</span><span class="sxs-lookup"><span data-stu-id="384ff-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="384ff-508">При подключении отобразилась ошибка с кодом 403</span><span class="sxs-lookup"><span data-stu-id="384ff-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-509">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-509">Probable causes</span></span>
* <span data-ttu-id="384ff-510">Hello Дата и время неверны на сервере Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="384ff-511">Hello идентификатор рабочей области и ключ рабочей области, используемый неверны</span><span class="sxs-lookup"><span data-stu-id="384ff-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="384ff-512">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="384ff-512">Resolution</span></span>
* <span data-ttu-id="384ff-513">Проверьте время hello на сервер Linux с hello `date` команды.</span><span class="sxs-lookup"><span data-stu-id="384ff-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="384ff-514">Если приветствия данные больше или меньше, чем 15 минут с момента hello текущее время, адаптации завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="384ff-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="384ff-515">toocorrect, Обновить дату hello и часовой пояс сервера Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="384ff-516">последнюю версию агента OMS для Linux hello Hello уведомляет пользователя, если разница во времени является причиной сбоя адаптации</span><span class="sxs-lookup"><span data-stu-id="384ff-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="384ff-517">RE регистрации с помощью hello правильный идентификатор рабочей области и ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="384ff-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="384ff-518">В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="384ff-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="384ff-519">Ошибка 500 или сообщение об ошибке 404 указывается в файле журнала hello после адаптации</span><span class="sxs-lookup"><span data-stu-id="384ff-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="384ff-520">Это известная проблема, возникающая во время первой передачи данных Linux в рабочей области OMS hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="384ff-521">Это не влияет на отправляемые данные и не вызывает другие проблемы.</span><span class="sxs-lookup"><span data-stu-id="384ff-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="384ff-522">Можно проигнорировать ошибки hello при первоначальном адаптации.</span><span class="sxs-lookup"><span data-stu-id="384ff-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="384ff-523">Nagios данных не отображается в hello портал OMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-524">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-524">Probable causes</span></span>
* <span data-ttu-id="384ff-525">Hello omsagent пользователь не имеет разрешения tooread из файла журнала Nagios hello</span><span class="sxs-lookup"><span data-stu-id="384ff-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="384ff-526">Hello Nagios источника и фильтр разделы по-прежнему закомментированы в файле omsagent.conf hello</span><span class="sxs-lookup"><span data-stu-id="384ff-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-527">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-527">Resolutions</span></span>
* <span data-ttu-id="384ff-528">Добавьте пользователя omsagent hello в порядке tooread из файла Nagios hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="384ff-529">Дополнительные сведения см. в разделе об [оповещениях Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts).</span><span class="sxs-lookup"><span data-stu-id="384ff-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="384ff-530">В hello агента OMS для Linux файла общие конфигурации на `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, убедитесь, что **оба** hello Nagios источника и фильтровать раздела имеют примечания удалены, аналогичные toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="384ff-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="384ff-531">Не обновляются данные Linux hello портал OMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-532">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-532">Probable causes</span></span>
* <span data-ttu-id="384ff-533">Не удалось выполнить toohello адаптации службой OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="384ff-534">Заблокированные соединения toohello службой OMS</span><span class="sxs-lookup"><span data-stu-id="384ff-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="384ff-535">Hello агента OMS для Linux данных резервных копий</span><span class="sxs-lookup"><span data-stu-id="384ff-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-536">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-536">Resolutions</span></span>
* <span data-ttu-id="384ff-537">Убедитесь, что toohello адаптации службой OMS, проверяя, hello успешно `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` существует.</span><span class="sxs-lookup"><span data-stu-id="384ff-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="384ff-538">RE регистрации с помощью hello omsadmin.sh командной строки.</span><span class="sxs-lookup"><span data-stu-id="384ff-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="384ff-539">В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="384ff-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="384ff-540">При использовании прокси-сервера используйте hello прокси действия по устранению неполадок выше</span><span class="sxs-lookup"><span data-stu-id="384ff-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="384ff-541">В некоторых случаях если hello агента OMS для Linux не может взаимодействовать со службой OMS hello данные на hello агента — размер полный буфер toohello резервную копию 50 МБ.</span><span class="sxs-lookup"><span data-stu-id="384ff-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="384ff-542">Перезапустите hello агента OMS для Linux с помощью hello `/opt/microsoft/omsagent/bin/service_control restart` команды.</span><span class="sxs-lookup"><span data-stu-id="384ff-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="384ff-543">Эта проблема исправлена в агенте версии 1.1.0-28 и выше.</span><span class="sxs-lookup"><span data-stu-id="384ff-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="384ff-544">Конфигурация счетчиков производительности syslog Linux не применяется на портале OMS hello</span><span class="sxs-lookup"><span data-stu-id="384ff-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-545">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-545">Probable causes</span></span>
* <span data-ttu-id="384ff-546">агент конфигурации Hello в hello агента OMS для Linux не получен hello последнюю конфигурацию из портала OMS hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="384ff-547">Hello измененные параметры портала hello не были применены</span><span class="sxs-lookup"><span data-stu-id="384ff-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-548">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-548">Resolutions</span></span>
<span data-ttu-id="384ff-549">`omsconfig`— агент конфигурации hello в hello агента OMS для Linux, который получает изменения конфигурации портала OMS каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="384ff-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="384ff-550">Эта конфигурация будет применен toohello агента OMS для Linux файлов конфигурации, расположенный `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="384ff-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="384ff-551">В некоторых случаях hello агента OMS для Linux конфигурации агента может оказаться может toocommunicate со службой настройки портала hello приведет к последней конфигурации не применяются.</span><span class="sxs-lookup"><span data-stu-id="384ff-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="384ff-552">Убедитесь, что hello `omsconfig` агент установлен hello следующее:</span><span class="sxs-lookup"><span data-stu-id="384ff-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="384ff-553">`dpkg --list omsconfig` или `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="384ff-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="384ff-554">Если не установлен, установите последнюю версию hello hello агента OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="384ff-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="384ff-555">Убедитесь, что hello `omsconfig` агент может взаимодействовать со службой OMS hello</span><span class="sxs-lookup"><span data-stu-id="384ff-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="384ff-556">Запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` команды</span><span class="sxs-lookup"><span data-stu-id="384ff-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="384ff-557">Hello выше команда возвращает hello конфигурацию, агент получает из портала hello, включая параметры Syslog, счетчики производительности Linux и пользовательских журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="384ff-558">Если команда hello выше не выполняется, запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` команды.</span><span class="sxs-lookup"><span data-stu-id="384ff-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="384ff-559">Эта команда принудительно выполняет toocommunicate агента omsconfig hello с последней конфигурацией hello OMS службы tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="384ff-560">Пользовательские данные журнала Linux не отображается в hello портал OMS.</span><span class="sxs-lookup"><span data-stu-id="384ff-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="384ff-561">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="384ff-561">Probable causes</span></span>
* <span data-ttu-id="384ff-562">Сбой службы адаптации tooOMS</span><span class="sxs-lookup"><span data-stu-id="384ff-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="384ff-563">Hello **hello применить следующие конфигурации toomy серверы Linux** параметр не выбран</span><span class="sxs-lookup"><span data-stu-id="384ff-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="384ff-564">omsconfig не подбираются hello последнюю пользовательский журнал с портала hello</span><span class="sxs-lookup"><span data-stu-id="384ff-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="384ff-565">Hello `omsagent` используется пользовательский журнал hello tooaccess не удается из-за проблемы разрешения tooa или `omsagent` не найден.</span><span class="sxs-lookup"><span data-stu-id="384ff-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="384ff-566">В этом случае вы увидите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="384ff-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="384ff-567">Это известная проблема с hello гонки, которая была исправлена в hello агента OMS для Linux версии 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="384ff-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="384ff-568">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="384ff-568">Resolutions</span></span>
* <span data-ttu-id="384ff-569">Убедитесь, что вы успешно встроен, определяя, является ли hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` файл существует.</span><span class="sxs-lookup"><span data-stu-id="384ff-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="384ff-570">При необходимости, регистрации снова с помощью командной строки omsadmin.sh hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="384ff-571">В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="384ff-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="384ff-572">В hello портал OMS. в разделе **параметры** на hello **данные** убедитесь, что hello **hello применить следующие конфигурации toomy серверы Linux** выбран параметр</span><span class="sxs-lookup"><span data-stu-id="384ff-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="384ff-573">![Применить конфигурацию](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="384ff-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="384ff-574">Убедитесь, что hello `omsconfig` агент может взаимодействовать со службой OMS hello</span><span class="sxs-lookup"><span data-stu-id="384ff-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="384ff-575">Запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` команды</span><span class="sxs-lookup"><span data-stu-id="384ff-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="384ff-576">Hello выше команда возвращает hello конфигурацию, агент получает из hello портал, включая параметры Syslog, счетчики производительности Linux и пользовательских журналов</span><span class="sxs-lookup"><span data-stu-id="384ff-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="384ff-577">Если команда hello выше не выполняется, запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` команды.</span><span class="sxs-lookup"><span data-stu-id="384ff-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="384ff-578">Эта команда принудительно toocommunicate агента omsconfig hello со службой OMS и получить последнюю конфигурацию hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="384ff-579">Вместо hello агента OMS для работы в качестве пользователя с правами доступа пользователя Linux `root`, hello агента OMS для Linux, выполняется как hello `omsagent` пользователя.</span><span class="sxs-lookup"><span data-stu-id="384ff-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="384ff-580">В большинстве случаев явное разрешение должно быть предоставлено toohello пользователя в порядке tooread некоторые файлы.</span><span class="sxs-lookup"><span data-stu-id="384ff-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="384ff-581">разрешение toogrant слишком`omsagent` пользователя, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="384ff-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="384ff-582">Добавить hello `omsagent` определенной группе пользователей tooa с`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="384ff-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="384ff-583">Предоставьте необходимый файл toohello универсальный доступ на чтение с`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="384ff-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="384ff-584">Имеется известная проблема с hello гонки, которая была исправлена в hello агента OMS для Linux 1.1.0-217 версии.</span><span class="sxs-lookup"><span data-stu-id="384ff-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="384ff-585">После обновления toohello последнюю версию агента, выполните hello, следующая команда tooget hello последнюю версию подключаемого модуля hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="384ff-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="384ff-586">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="384ff-586">Known limitations</span></span>
<span data-ttu-id="384ff-587">Просмотрите следующие разделы toolearn о текущих ограничений hello агента OMS для Linux hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="384ff-588">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="384ff-588">Azure Diagnostics</span></span>
<span data-ttu-id="384ff-589">Для виртуальных машин Linux, работающих в Azure дополнительные действия могут быть tooallow требуется сбор данных диагностики Azure и Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="384ff-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="384ff-590">**Версии 2.2** hello диагностическое расширение является обязательным для совместимости с hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="384ff-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="384ff-591">Дополнительные сведения об установке и настройке hello диагностического расширения для Linux см. в разделе [использовать hello Azure CLI команда tooenable диагностического расширения для Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="384ff-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="384ff-592">**Обновление 2.0 too2.2 интерфейсе командной строки Azure ASM hello диагностического расширения для Linux:**</span><span class="sxs-lookup"><span data-stu-id="384ff-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="384ff-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="384ff-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="384ff-594">В этих примерах команд указан файл PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="384ff-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="384ff-595">Hello формат этого файла должен быть похож на следующий образец hello.</span><span class="sxs-lookup"><span data-stu-id="384ff-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="384ff-596">sysklog не поддерживается</span><span class="sxs-lookup"><span data-stu-id="384ff-596">Sysklog is not supported</span></span>
<span data-ttu-id="384ff-597">Rsyslog или syslog-ng, требуется toocollect syslog-сообщения.</span><span class="sxs-lookup"><span data-stu-id="384ff-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="384ff-598">управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog.</span><span class="sxs-lookup"><span data-stu-id="384ff-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="384ff-599">toocollect данных syslog из этой версии данных дистрибутивов hello rsyslog управляющая программа должна быть установлена и настроена tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="384ff-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="384ff-600">Дополнительные сведения о замене sysklog на rsyslog см. в разделе [Установка hello вновь созданного пакета RPM rsyslog](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="384ff-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="384ff-601">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="384ff-601">Next Steps</span></span>
* <span data-ttu-id="384ff-602">[Добавление решений анализа журналов из коллекции решений hello](log-analytics-add-solutions.md) tooadd функциональные возможности и сбора данных.</span><span class="sxs-lookup"><span data-stu-id="384ff-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="384ff-603">Ознакомьтесь с [входа выполняет](log-analytics-log-searches.md) tooview подробные данные, собранные решения.</span><span class="sxs-lookup"><span data-stu-id="384ff-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="384ff-604">Используйте [панелей мониторинга](log-analytics-dashboards.md) toosave и отображения выполняет собственную.</span><span class="sxs-lookup"><span data-stu-id="384ff-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
