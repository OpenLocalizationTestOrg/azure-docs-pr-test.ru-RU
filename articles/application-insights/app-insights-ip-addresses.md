---
title: "aaaIP адреса, используемые Application Insights | Документы Microsoft"
description: "Исключения брандмауэра сервера, требуемые для Application Insights"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="df70f-103">IP-адреса, используемые службой Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="df70f-104">Hello [Azure Application Insights](app-insights-overview.md) служба использует несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="df70f-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="df70f-105">Может потребоваться эти адреса tooknow, если приложение hello, которое вы наблюдаете находится за брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="df70f-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="df70f-106">Несмотря на то, что эти адреса являются статическими, это возможно, что нам нужно будет toochange их tootime времени.</span><span class="sxs-lookup"><span data-stu-id="df70f-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="df70f-107">Порты для исходящего трафика</span><span class="sxs-lookup"><span data-stu-id="df70f-107">Outgoing ports</span></span>
<span data-ttu-id="df70f-108">Требуется tooopen некоторые исходящие порты в hello tooallow брандмауэра сервера пакет SDK Application Insights и/или данные toohello монитор состояния toosend портала:</span><span class="sxs-lookup"><span data-stu-id="df70f-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="df70f-109">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-109">Purpose</span></span> | <span data-ttu-id="df70f-110">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-110">URL</span></span> | <span data-ttu-id="df70f-111">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-111">IP</span></span> | <span data-ttu-id="df70f-112">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-113">Телеметрия</span><span class="sxs-lookup"><span data-stu-id="df70f-113">Telemetry</span></span> |<span data-ttu-id="df70f-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="df70f-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="df70f-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="df70f-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="df70f-116">40.114.241.141</span></span><br/><span data-ttu-id="df70f-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="df70f-117">104.45.136.42</span></span><br/><span data-ttu-id="df70f-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="df70f-118">40.84.189.107</span></span><br/><span data-ttu-id="df70f-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="df70f-119">168.63.242.221</span></span><br/><span data-ttu-id="df70f-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="df70f-120">52.167.221.184</span></span><br/><span data-ttu-id="df70f-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="df70f-121">52.169.64.244</span></span> |<span data-ttu-id="df70f-122">443</span><span class="sxs-lookup"><span data-stu-id="df70f-122">443</span></span> |
| <span data-ttu-id="df70f-123">Динамический поток метрик</span><span class="sxs-lookup"><span data-stu-id="df70f-123">Live Metrics Stream</span></span> |<span data-ttu-id="df70f-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="df70f-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="df70f-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="df70f-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="df70f-126">23.96.28.38</span></span><br/><span data-ttu-id="df70f-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="df70f-127">13.92.40.198</span></span> |<span data-ttu-id="df70f-128">443</span><span class="sxs-lookup"><span data-stu-id="df70f-128">443</span></span> |
| <span data-ttu-id="df70f-129">Внутренняя телеметрия</span><span class="sxs-lookup"><span data-stu-id="df70f-129">Internal Telemetry</span></span> |<span data-ttu-id="df70f-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="df70f-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="df70f-131">52.161.11.71</span></span> |<span data-ttu-id="df70f-132">443</span><span class="sxs-lookup"><span data-stu-id="df70f-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="df70f-133">Монитор состояния</span><span class="sxs-lookup"><span data-stu-id="df70f-133">Status Monitor</span></span>
<span data-ttu-id="df70f-134">Настройка монитора состояния (требуется только для внесения изменений).</span><span class="sxs-lookup"><span data-stu-id="df70f-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="df70f-135">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-135">Purpose</span></span> | <span data-ttu-id="df70f-136">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-136">URL</span></span> | <span data-ttu-id="df70f-137">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-137">IP</span></span> | <span data-ttu-id="df70f-138">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-139">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="df70f-140">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="df70f-141">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="df70f-142">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="df70f-143">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="df70f-144">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="df70f-145">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="df70f-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="df70f-146">Установка</span><span class="sxs-lookup"><span data-stu-id="df70f-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="df70f-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="df70f-147">HockeyApp</span></span>
| <span data-ttu-id="df70f-148">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-148">Purpose</span></span> | <span data-ttu-id="df70f-149">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-149">URL</span></span> | <span data-ttu-id="df70f-150">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-150">IP</span></span> | <span data-ttu-id="df70f-151">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-152">Данные о сбоях</span><span class="sxs-lookup"><span data-stu-id="df70f-152">Crash data</span></span> |<span data-ttu-id="df70f-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="df70f-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="df70f-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="df70f-154">104.45.136.42</span></span> |<span data-ttu-id="df70f-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="df70f-156">Тесты доступности</span><span class="sxs-lookup"><span data-stu-id="df70f-156">Availability tests</span></span>
<span data-ttu-id="df70f-157">Это список адресов, из которого hello [доступности веб-тесты](app-insights-monitor-web-app-availability.md) выполняются.</span><span class="sxs-lookup"><span data-stu-id="df70f-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="df70f-158">Если вы хотите toorun веб-тестов в приложении, но веб-сервера имеет ограниченные tooserving конкретных клиентов, будет иметь toopermit входящий трафик от наших доступности тестовые серверы.</span><span class="sxs-lookup"><span data-stu-id="df70f-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="df70f-159">Откройте порты 80 (HTTP) и 443 (HTTPS) для входящего трафика с этих адресов (IP-адреса сгруппированы по расположению):</span><span class="sxs-lookup"><span data-stu-id="df70f-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="df70f-160">API доступа к данным</span><span class="sxs-lookup"><span data-stu-id="df70f-160">Data access API</span></span>
| <span data-ttu-id="df70f-161">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-161">Purpose</span></span> | <span data-ttu-id="df70f-162">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-162">URI</span></span> | <span data-ttu-id="df70f-163">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-163">IP</span></span> | <span data-ttu-id="df70f-164">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-165">API</span><span class="sxs-lookup"><span data-stu-id="df70f-165">API</span></span> |<span data-ttu-id="df70f-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="df70f-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="df70f-172">13.82.26.252</span></span><br/><span data-ttu-id="df70f-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="df70f-173">40.76.213.73</span></span> |<span data-ttu-id="df70f-174">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-174">80,443</span></span> |
| <span data-ttu-id="df70f-175">Документация по API</span><span class="sxs-lookup"><span data-stu-id="df70f-175">API docs</span></span> |<span data-ttu-id="df70f-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="df70f-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="df70f-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="df70f-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="df70f-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="df70f-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="df70f-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="df70f-182">13.82.24.149</span></span><br/><span data-ttu-id="df70f-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="df70f-183">40.114.82.10</span></span> |<span data-ttu-id="df70f-184">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-184">80,443</span></span> |
| <span data-ttu-id="df70f-185">Внутренний API</span><span class="sxs-lookup"><span data-stu-id="df70f-185">Internal API</span></span> |<span data-ttu-id="df70f-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="df70f-193">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-193">dynamic</span></span>|<span data-ttu-id="df70f-194">443</span><span class="sxs-lookup"><span data-stu-id="df70f-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="df70f-195">Аналитика Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-195">Application Insights Analytics</span></span>

| <span data-ttu-id="df70f-196">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-196">Purpose</span></span> | <span data-ttu-id="df70f-197">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-197">URI</span></span> | <span data-ttu-id="df70f-198">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-198">IP</span></span> | <span data-ttu-id="df70f-199">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-200">Портал аналитики</span><span class="sxs-lookup"><span data-stu-id="df70f-200">Analytics Portal</span></span> | <span data-ttu-id="df70f-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="df70f-202">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-202">dynamic</span></span> | <span data-ttu-id="df70f-203">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-203">80,443</span></span> |
| <span data-ttu-id="df70f-204">CDN</span><span class="sxs-lookup"><span data-stu-id="df70f-204">CDN</span></span> | <span data-ttu-id="df70f-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="df70f-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="df70f-206">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-206">dynamic</span></span> | <span data-ttu-id="df70f-207">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-207">80,443</span></span> |
| <span data-ttu-id="df70f-208">Мультимедиа CDN</span><span class="sxs-lookup"><span data-stu-id="df70f-208">Media CDN</span></span> | <span data-ttu-id="df70f-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="df70f-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="df70f-210">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-210">dynamic</span></span> | <span data-ttu-id="df70f-211">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-211">80,443</span></span> |

<span data-ttu-id="df70f-212">Примечание. Домен applicationinsights.io принадлежит команде Application Insights.</span><span class="sxs-lookup"><span data-stu-id="df70f-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="df70f-213">Расширение портала Azure для Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="df70f-214">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-214">Purpose</span></span> | <span data-ttu-id="df70f-215">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-215">URI</span></span> | <span data-ttu-id="df70f-216">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-216">IP</span></span> | <span data-ttu-id="df70f-217">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-218">Расширение для Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-218">Application Insights Extension</span></span> | <span data-ttu-id="df70f-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="df70f-220">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-220">dynamic</span></span> | <span data-ttu-id="df70f-221">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-221">80,443</span></span> |
| <span data-ttu-id="df70f-222">Расширение CDN для Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="df70f-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="df70f-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="df70f-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="df70f-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="df70f-226">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-226">dynamic</span></span> | <span data-ttu-id="df70f-227">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="df70f-228">Пакеты средств разработки Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-228">Application Insights SDKs</span></span>

| <span data-ttu-id="df70f-229">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-229">Purpose</span></span> | <span data-ttu-id="df70f-230">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-230">URI</span></span> | <span data-ttu-id="df70f-231">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-231">IP</span></span> | <span data-ttu-id="df70f-232">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-233">Пакеты средств разработки CDN JS Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="df70f-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="df70f-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="df70f-235">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-235">dynamic</span></span> | <span data-ttu-id="df70f-236">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-236">80,443</span></span> |
| <span data-ttu-id="df70f-237">Пакеты средств разработки Java Application Insights</span><span class="sxs-lookup"><span data-stu-id="df70f-237">Application Insights Java SDK</span></span> | <span data-ttu-id="df70f-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="df70f-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="df70f-239">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-239">dynamic</span></span> | <span data-ttu-id="df70f-240">80, 443</span><span class="sxs-lookup"><span data-stu-id="df70f-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="df70f-241">Профилировщик</span><span class="sxs-lookup"><span data-stu-id="df70f-241">Profiler</span></span>

| <span data-ttu-id="df70f-242">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-242">Purpose</span></span> | <span data-ttu-id="df70f-243">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-243">URI</span></span> | <span data-ttu-id="df70f-244">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-244">IP</span></span> | <span data-ttu-id="df70f-245">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-246">Агент</span><span class="sxs-lookup"><span data-stu-id="df70f-246">Agent</span></span> | <span data-ttu-id="df70f-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="df70f-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="df70f-249">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-249">dynamic</span></span> | <span data-ttu-id="df70f-250">443</span><span class="sxs-lookup"><span data-stu-id="df70f-250">443</span></span>
| <span data-ttu-id="df70f-251">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="df70f-251">Portal</span></span> | <span data-ttu-id="df70f-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="df70f-253">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-253">dynamic</span></span> | <span data-ttu-id="df70f-254">443</span><span class="sxs-lookup"><span data-stu-id="df70f-254">443</span></span>
| <span data-ttu-id="df70f-255">Хранилище</span><span class="sxs-lookup"><span data-stu-id="df70f-255">Storage</span></span> | <span data-ttu-id="df70f-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="df70f-256">*.core.windows.net</span></span> | <span data-ttu-id="df70f-257">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-257">dynamic</span></span> | <span data-ttu-id="df70f-258">443</span><span class="sxs-lookup"><span data-stu-id="df70f-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="df70f-259">Отладчик моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="df70f-259">Snapshot Debugger</span></span>

| <span data-ttu-id="df70f-260">Назначение</span><span class="sxs-lookup"><span data-stu-id="df70f-260">Purpose</span></span> | <span data-ttu-id="df70f-261">URI</span><span class="sxs-lookup"><span data-stu-id="df70f-261">URI</span></span> | <span data-ttu-id="df70f-262">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="df70f-262">IP</span></span> | <span data-ttu-id="df70f-263">порты;</span><span class="sxs-lookup"><span data-stu-id="df70f-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df70f-264">Агент</span><span class="sxs-lookup"><span data-stu-id="df70f-264">Agent</span></span> | <span data-ttu-id="df70f-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="df70f-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="df70f-267">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-267">dynamic</span></span> | <span data-ttu-id="df70f-268">443</span><span class="sxs-lookup"><span data-stu-id="df70f-268">443</span></span>
| <span data-ttu-id="df70f-269">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="df70f-269">Portal</span></span> | <span data-ttu-id="df70f-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="df70f-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="df70f-271">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-271">dynamic</span></span> | <span data-ttu-id="df70f-272">443</span><span class="sxs-lookup"><span data-stu-id="df70f-272">443</span></span>
| <span data-ttu-id="df70f-273">Хранилище</span><span class="sxs-lookup"><span data-stu-id="df70f-273">Storage</span></span> | <span data-ttu-id="df70f-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="df70f-274">*.core.windows.net</span></span> | <span data-ttu-id="df70f-275">Динамический</span><span class="sxs-lookup"><span data-stu-id="df70f-275">dynamic</span></span> | <span data-ttu-id="df70f-276">443</span><span class="sxs-lookup"><span data-stu-id="df70f-276">443</span></span>
