---
title: "aaaAzure архитектура подключения к базе данных SQL | Документы Microsoft"
description: "В этом документе описывается hello Azure SQLDB подключения архитектура из Azure или из за пределами Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="825a9-103">Архитектура подключений к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="825a9-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="825a9-104">В этой статье описывается архитектура подключения к базе данных SQL Azure hello и объясняется, как различные компоненты hello функции toodirect трафика tooyour экземпляра базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="825a9-105">Эти компоненты подключения к базе данных SQL Azure функцию toodirect сетевой трафик toohello базы данных SQL Azure с клиентов, подключающихся с в Azure и клиентов, подключающихся с за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="825a9-106">В этой статье также предоставляет toochange образцы сценариев, как выполняется подключение, и вопросы hello связанные параметры подключения по умолчанию hello toochanging.</span><span class="sxs-lookup"><span data-stu-id="825a9-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="825a9-107">В случае возникновения вопросов после прочтения этой статьи вы можете обратиться к Дхруву Малику, написав на электронный адрес dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="825a9-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="825a9-108">Архитектура подключения</span><span class="sxs-lookup"><span data-stu-id="825a9-108">Connectivity architecture</span></span>

<span data-ttu-id="825a9-109">Следующая схема Hello предоставляет высокоуровневый обзор hello архитектура подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="825a9-111">Hello следующие шаги описывают как соединение имеет установленное tooan базы данных Azure SQL через hello базы данных SQL Azure программного обеспечения нагрузки-подсистемы балансировки и шлюза hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="825a9-112">Клиенты в пределах Azure или за пределами Azure подключаться toohello по, который содержит общедоступный IP-адрес и прослушивает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="825a9-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="825a9-113">Hello по направляет трафик toohello базы данных SQL Azure шлюза.</span><span class="sxs-lookup"><span data-stu-id="825a9-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="825a9-114">шлюз Hello перенаправляет hello трафика toohello подходящий посредник по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="825a9-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="825a9-115">по промежуточного слоя Hello прокси перенаправляет hello трафика toohello соответствующей базы, данных с Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="825a9-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="825a9-116">Каждый из этих компонентов с распределенными отказ защиты службы (DDoS), встроенные в сети hello и уровня приложения hello.</span><span class="sxs-lookup"><span data-stu-id="825a9-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="825a9-117">Подключение из Azure</span><span class="sxs-lookup"><span data-stu-id="825a9-117">Connectivity from within Azure</span></span>

<span data-ttu-id="825a9-118">Для подключений из Azure по умолчанию действует политика подключения **Перенаправление**.</span><span class="sxs-lookup"><span data-stu-id="825a9-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="825a9-119">Политику **перенаправления** означает, что соединения после сеанса TCP hello установленного toohello базы данных Azure SQL, hello клиентский сеанс, а затем перенаправление по промежуточного слоя прокси toohello с изменение toohello назначения виртуальных IP-адрес из что toothat шлюза hello базы данных SQL Azure по промежуточного слоя hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="825a9-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="825a9-120">После этого все последующие пакеты потока непосредственно через hello прокси-сервера по промежуточного слоя, минуя hello шлюза базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="825a9-121">Привет, следующая схема иллюстрирует этот поток трафика.</span><span class="sxs-lookup"><span data-stu-id="825a9-121">hello following diagram illustrates this traffic flow.</span></span>

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="825a9-123">Подключение извне Azure</span><span class="sxs-lookup"><span data-stu-id="825a9-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="825a9-124">Для подключений извне Azure по умолчанию действует политика подключения **Прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="825a9-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="825a9-125">Политику **прокси** означает, что сеанс TCP hello устанавливается через шлюз базы данных SQL Azure hello и все последующие пакеты потока через hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="825a9-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="825a9-126">Привет, следующая схема иллюстрирует этот поток трафика.</span><span class="sxs-lookup"><span data-stu-id="825a9-126">hello following diagram illustrates this traffic flow.</span></span>

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="825a9-128">IP-адреса шлюза базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="825a9-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="825a9-129">tooconnect tooan базы данных SQL Azure с локальными ресурсами, необходима tooallow исходящий сетевой трафик toohello базы данных SQL Azure шлюза ваш регион Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="825a9-130">Подключения перейдите через шлюз hello, при подключении в режиме прокси-сервера, который является по умолчанию hello при соединении с локальными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="825a9-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="825a9-131">Привет, в следующей таблице перечислены hello основного и дополнительного IP-адреса шлюза hello базы данных SQL Azure для всех областей данных.</span><span class="sxs-lookup"><span data-stu-id="825a9-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="825a9-132">В некоторых регионах существует два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="825a9-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="825a9-133">В этих областях hello основной IP-адрес является hello текущий IP-адрес шлюза hello и hello второй IP-адрес — переход на другой ресурс IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="825a9-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="825a9-134">адрес перехода на другой ресурс Hello-toowhich адрес hello мы возможно перемещение сервера tookeep hello доступность службы высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="825a9-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="825a9-135">Для этих областей рекомендуется разрешить исходящие tooboth hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="825a9-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="825a9-136">Hello второй IP-адрес принадлежит корпорации Майкрософт и не прослушивает любые службы, пока она активируется соединениями tooaccept базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="825a9-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="825a9-137">Имя региона</span><span class="sxs-lookup"><span data-stu-id="825a9-137">Region Name</span></span> | <span data-ttu-id="825a9-138">Основной IP-адрес</span><span class="sxs-lookup"><span data-stu-id="825a9-138">Primary IP address</span></span> | <span data-ttu-id="825a9-139">Дополнительный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="825a9-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="825a9-140">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="825a9-140">Australia East</span></span> | <span data-ttu-id="825a9-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="825a9-141">191.238.66.109</span></span> | <span data-ttu-id="825a9-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="825a9-142">13.75.149.87</span></span> |
| <span data-ttu-id="825a9-143">Юго-Восточная Австралия</span><span class="sxs-lookup"><span data-stu-id="825a9-143">Australia South East</span></span> | <span data-ttu-id="825a9-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="825a9-144">191.239.192.109</span></span> | <span data-ttu-id="825a9-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="825a9-145">13.73.109.251</span></span> |
| <span data-ttu-id="825a9-146">Южная часть Бразилии</span><span class="sxs-lookup"><span data-stu-id="825a9-146">Brazil South</span></span> | <span data-ttu-id="825a9-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="825a9-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="825a9-148">Центральная Канада</span><span class="sxs-lookup"><span data-stu-id="825a9-148">Canada Central</span></span> | <span data-ttu-id="825a9-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="825a9-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="825a9-150">Восточная Канада</span><span class="sxs-lookup"><span data-stu-id="825a9-150">Canada East</span></span> | <span data-ttu-id="825a9-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="825a9-151">40.86.226.166</span></span> | |
| <span data-ttu-id="825a9-152">Центральный регион США</span><span class="sxs-lookup"><span data-stu-id="825a9-152">Central US</span></span> | <span data-ttu-id="825a9-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="825a9-153">23.99.160.139</span></span> | <span data-ttu-id="825a9-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="825a9-154">13.67.215.62</span></span> |
| <span data-ttu-id="825a9-155">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="825a9-155">East Asia</span></span> | <span data-ttu-id="825a9-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="825a9-156">191.234.2.139</span></span> | <span data-ttu-id="825a9-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="825a9-157">52.175.33.150</span></span> |
| <span data-ttu-id="825a9-158">Восточная часть США 1</span><span class="sxs-lookup"><span data-stu-id="825a9-158">East US 1</span></span> | <span data-ttu-id="825a9-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="825a9-159">191.238.6.43</span></span> | <span data-ttu-id="825a9-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="825a9-160">40.121.158.30</span></span> |
| <span data-ttu-id="825a9-161">Восток США 2</span><span class="sxs-lookup"><span data-stu-id="825a9-161">East US 2</span></span> | <span data-ttu-id="825a9-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="825a9-162">191.239.224.107</span></span> | <span data-ttu-id="825a9-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="825a9-163">40.79.84.180</span></span> |
| <span data-ttu-id="825a9-164">Центральная Индия</span><span class="sxs-lookup"><span data-stu-id="825a9-164">India Central</span></span> | <span data-ttu-id="825a9-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="825a9-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="825a9-166">Южная Индия</span><span class="sxs-lookup"><span data-stu-id="825a9-166">India South</span></span> | <span data-ttu-id="825a9-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="825a9-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="825a9-168">Западная Индия</span><span class="sxs-lookup"><span data-stu-id="825a9-168">India West</span></span> | <span data-ttu-id="825a9-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="825a9-169">104.211.160.80</span></span> | |
| <span data-ttu-id="825a9-170">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="825a9-170">Japan East</span></span> | <span data-ttu-id="825a9-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="825a9-171">191.237.240.43</span></span> | <span data-ttu-id="825a9-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="825a9-172">13.78.61.196</span></span> |
| <span data-ttu-id="825a9-173">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="825a9-173">Japan West</span></span> | <span data-ttu-id="825a9-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="825a9-174">191.238.68.11</span></span> | <span data-ttu-id="825a9-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="825a9-175">104.214.148.156</span></span> |
| <span data-ttu-id="825a9-176">Центральная Корея</span><span class="sxs-lookup"><span data-stu-id="825a9-176">Korea Central</span></span> | <span data-ttu-id="825a9-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="825a9-177">52.231.32.42</span></span> | |
| <span data-ttu-id="825a9-178">Южная Корея</span><span class="sxs-lookup"><span data-stu-id="825a9-178">Korea South</span></span> | <span data-ttu-id="825a9-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="825a9-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="825a9-180">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="825a9-180">North Central US</span></span> | <span data-ttu-id="825a9-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="825a9-181">23.98.55.75</span></span> | <span data-ttu-id="825a9-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="825a9-182">23.96.178.199</span></span> |
| <span data-ttu-id="825a9-183">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="825a9-183">North Europe</span></span> | <span data-ttu-id="825a9-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="825a9-184">191.235.193.75</span></span> | <span data-ttu-id="825a9-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="825a9-185">40.113.93.91</span></span> |
| <span data-ttu-id="825a9-186">Южно-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="825a9-186">South Central US</span></span> | <span data-ttu-id="825a9-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="825a9-187">23.98.162.75</span></span> | <span data-ttu-id="825a9-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="825a9-188">13.66.62.124</span></span> |
| <span data-ttu-id="825a9-189">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="825a9-189">South East Asia</span></span> | <span data-ttu-id="825a9-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="825a9-190">23.100.117.95</span></span> | <span data-ttu-id="825a9-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="825a9-191">104.43.15.0</span></span> |
| <span data-ttu-id="825a9-192">Север Соединенного Королевства</span><span class="sxs-lookup"><span data-stu-id="825a9-192">UK North</span></span> | <span data-ttu-id="825a9-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="825a9-193">13.87.97.210</span></span> | |
| <span data-ttu-id="825a9-194">Южная часть Соединенного Королевства 1</span><span class="sxs-lookup"><span data-stu-id="825a9-194">UK South 1</span></span> | <span data-ttu-id="825a9-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="825a9-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="825a9-196">Юг Соединенного Королевства 2</span><span class="sxs-lookup"><span data-stu-id="825a9-196">UK South 2</span></span> | <span data-ttu-id="825a9-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="825a9-197">13.87.34.7</span></span> | |
| <span data-ttu-id="825a9-198">Западная часть Великобритании</span><span class="sxs-lookup"><span data-stu-id="825a9-198">UK West</span></span> | <span data-ttu-id="825a9-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="825a9-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="825a9-200">Западно-центральная часть США</span><span class="sxs-lookup"><span data-stu-id="825a9-200">West Central US</span></span> | <span data-ttu-id="825a9-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="825a9-201">13.78.145.25</span></span> | |
| <span data-ttu-id="825a9-202">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="825a9-202">West Europe</span></span> | <span data-ttu-id="825a9-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="825a9-203">191.237.232.75</span></span> | <span data-ttu-id="825a9-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="825a9-204">40.68.37.158</span></span> |
| <span data-ttu-id="825a9-205">Западная часть США 1</span><span class="sxs-lookup"><span data-stu-id="825a9-205">West US 1</span></span> | <span data-ttu-id="825a9-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="825a9-206">23.99.34.75</span></span> | <span data-ttu-id="825a9-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="825a9-207">104.42.238.205</span></span> |
| <span data-ttu-id="825a9-208">Западный регион США 2</span><span class="sxs-lookup"><span data-stu-id="825a9-208">West US 2</span></span> | <span data-ttu-id="825a9-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="825a9-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="825a9-210">Изменение политики подключения для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="825a9-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="825a9-211">hello toochange политики подключение базы данных SQL Azure для сервера базы данных SQL Azure, используйте hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="825a9-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="825a9-212">Если политика подключения настроена слишком**прокси-сервера**, всех сетевых пакетов потока через шлюз базы данных SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="825a9-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="825a9-213">Для этого параметра нужен IP-адрес tooallow исходящих tooonly hello базы данных SQL Azure шлюза.</span><span class="sxs-lookup"><span data-stu-id="825a9-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="825a9-214">В режиме **Прокси-сервер** задержка выше, чем в режиме **Перенаправление**.</span><span class="sxs-lookup"><span data-stu-id="825a9-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="825a9-215">При настройке политики подключения **перенаправления**, все сетевые пакеты непосредственно потока toohello прокси по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="825a9-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="825a9-216">Для этого параметра необходимо tooallow исходящих toomultiple IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="825a9-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="825a9-217">Параметры подключения toochange сценария</span><span class="sxs-lookup"><span data-stu-id="825a9-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="825a9-218">Для этого сценария требуется hello [модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="825a9-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="825a9-219">Следующий сценарий PowerShell Hello показано, как toochange hello политику подключений.</span><span class="sxs-lookup"><span data-stu-id="825a9-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="825a9-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="825a9-220">Next steps</span></span>

- <span data-ttu-id="825a9-221">Сведения о том, как toochange hello политики подключение базы данных SQL Azure для сервера базы данных SQL Azure см. в разделе [Здравствуйте, создания или обновления политики подключение сервера с помощью API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="825a9-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="825a9-222">Сведения о поведении подключения к базе данных SQL Azure клиентов, использующих ADO.NET 4.5 или более поздней версии, см. в разделе [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="825a9-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="825a9-223">Общая информация о разработке приложений приведена в разделе [Обзор разработки приложений баз данных SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="825a9-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
