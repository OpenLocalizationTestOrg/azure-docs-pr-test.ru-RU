---
title: "Архитектура подключений к базе данных SQL Azure | Документация Майкрософт"
description: "В этом документе описывается архитектура подключений к базе данных SQL Azure из Azure или извне Azure."
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
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="c77b2-103">Архитектура подключений к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c77b2-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="c77b2-104">В этой статье описывается архитектура подключения к базе данных SQL Azure и объясняется, как функционируют различные компоненты при передаче трафика к вашему экземпляру базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="c77b2-105">Эти компоненты подключения к базе данных SQL Azure направляют сетевой трафик к базе данных Azure с помощью клиентов, подключающихся из Azure, и клиентов, подключающихся извне Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="c77b2-106">В этой статье также приведены примеры сценариев, позволяющие изменить параметры подключения, а также рекомендации по изменению параметров подключения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c77b2-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="c77b2-107">В случае возникновения вопросов после прочтения этой статьи вы можете обратиться к Дхруву Малику, написав на электронный адрес dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c77b2-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="c77b2-108">Архитектура подключения</span><span class="sxs-lookup"><span data-stu-id="c77b2-108">Connectivity architecture</span></span>

<span data-ttu-id="c77b2-109">На следующей схеме показана общая архитектура подключений к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="c77b2-111">Ниже описывается, как устанавливается подключение к базе данных SQL Azure с помощью программного балансировщика нагрузки (SLB) и шлюза базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="c77b2-112">Клиенты в среде Azure или за ее пределами подключаются к программному балансировщику нагрузки, который использует общедоступный IP-адрес и ожидает передачи данных через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="c77b2-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="c77b2-113">Программный балансировщик нагрузки направляет трафик в шлюз базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="c77b2-114">Шлюз перенаправляет трафик к соответствующему ПО промежуточного уровня прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c77b2-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="c77b2-115">Которое перенаправляет трафик в соответствующую базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c77b2-116">У каждого из этих компонентов есть встроенная защита от отказа в обслуживании (DDoS) на сетевом и прикладном уровнях.</span><span class="sxs-lookup"><span data-stu-id="c77b2-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="c77b2-117">Подключение из Azure</span><span class="sxs-lookup"><span data-stu-id="c77b2-117">Connectivity from within Azure</span></span>

<span data-ttu-id="c77b2-118">Для подключений из Azure по умолчанию действует политика подключения **Перенаправление**.</span><span class="sxs-lookup"><span data-stu-id="c77b2-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="c77b2-119">Политика подключения **Перенаправление** означает, что после установления сеанса TCP с базой данных SQL Azure сеанс клиента перенаправляется в ПО промежуточного уровня прокси-сервера с измененным виртуальным IP-адресом назначения, то есть вместо адреса шлюза базы данных SQL Azure указывается адрес ПО промежуточного уровня прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c77b2-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="c77b2-120">После этого все последующие пакеты передаются непосредственно через ПО промежуточного уровня прокси-сервера, минуя шлюз базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="c77b2-121">Этот поток трафика представлен на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="c77b2-121">The following diagram illustrates this traffic flow.</span></span>

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="c77b2-123">Подключение извне Azure</span><span class="sxs-lookup"><span data-stu-id="c77b2-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="c77b2-124">Для подключений извне Azure по умолчанию действует политика подключения **Прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="c77b2-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="c77b2-125">Политика **Прокси-сервер** означает, что устанавливается сеанс TCP через шлюз базы данных SQL Azure и все последующие пакеты проходят через этот шлюз.</span><span class="sxs-lookup"><span data-stu-id="c77b2-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="c77b2-126">Этот поток трафика представлен на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="c77b2-126">The following diagram illustrates this traffic flow.</span></span>

![Общий вид архитектуры](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="c77b2-128">IP-адреса шлюза базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c77b2-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="c77b2-129">Чтобы иметь возможность подключения к базе данных SQL Azure из локальных ресурсов, необходимо разрешить исходящий сетевой трафик к шлюзу базы данных SQL Azure для своего региона Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="c77b2-130">При подключении в режиме прокси-сервера, который используется по умолчанию при подключении из локальных ресурсов, подключения проходят только через шлюз.</span><span class="sxs-lookup"><span data-stu-id="c77b2-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="c77b2-131">В следующей таблице перечислены основные и дополнительные IP-адреса шлюза базы данных SQL Azure для всех областей данных.</span><span class="sxs-lookup"><span data-stu-id="c77b2-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="c77b2-132">В некоторых регионах существует два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c77b2-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="c77b2-133">В этих регионах основным IP-адресом является текущий IP-адрес шлюза, а второй IP-адрес — это IP-адрес отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="c77b2-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="c77b2-134">Адрес отработки отказа — это адрес, на который можно переместить сервер, чтобы сохранить высокий уровень доступности службы.</span><span class="sxs-lookup"><span data-stu-id="c77b2-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="c77b2-135">Для этих регионов рекомендуется разрешить исходящий трафик для обоих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c77b2-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="c77b2-136">Второй IP-адрес принадлежит корпорации Майкрософт и не ожидает передачи данных от каких-либо служб, пока не будет активирован базой данных SQL Azure для приема подключений.</span><span class="sxs-lookup"><span data-stu-id="c77b2-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="c77b2-137">Имя региона</span><span class="sxs-lookup"><span data-stu-id="c77b2-137">Region Name</span></span> | <span data-ttu-id="c77b2-138">Основной IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c77b2-138">Primary IP address</span></span> | <span data-ttu-id="c77b2-139">Дополнительный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c77b2-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="c77b2-140">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="c77b2-140">Australia East</span></span> | <span data-ttu-id="c77b2-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="c77b2-141">191.238.66.109</span></span> | <span data-ttu-id="c77b2-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="c77b2-142">13.75.149.87</span></span> |
| <span data-ttu-id="c77b2-143">Юго-Восточная Австралия</span><span class="sxs-lookup"><span data-stu-id="c77b2-143">Australia South East</span></span> | <span data-ttu-id="c77b2-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="c77b2-144">191.239.192.109</span></span> | <span data-ttu-id="c77b2-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="c77b2-145">13.73.109.251</span></span> |
| <span data-ttu-id="c77b2-146">Южная часть Бразилии</span><span class="sxs-lookup"><span data-stu-id="c77b2-146">Brazil South</span></span> | <span data-ttu-id="c77b2-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="c77b2-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="c77b2-148">Центральная Канада</span><span class="sxs-lookup"><span data-stu-id="c77b2-148">Canada Central</span></span> | <span data-ttu-id="c77b2-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="c77b2-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="c77b2-150">Восточная Канада</span><span class="sxs-lookup"><span data-stu-id="c77b2-150">Canada East</span></span> | <span data-ttu-id="c77b2-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="c77b2-151">40.86.226.166</span></span> | |
| <span data-ttu-id="c77b2-152">Центральный регион США</span><span class="sxs-lookup"><span data-stu-id="c77b2-152">Central US</span></span> | <span data-ttu-id="c77b2-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="c77b2-153">23.99.160.139</span></span> | <span data-ttu-id="c77b2-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="c77b2-154">13.67.215.62</span></span> |
| <span data-ttu-id="c77b2-155">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="c77b2-155">East Asia</span></span> | <span data-ttu-id="c77b2-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="c77b2-156">191.234.2.139</span></span> | <span data-ttu-id="c77b2-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="c77b2-157">52.175.33.150</span></span> |
| <span data-ttu-id="c77b2-158">Восточная часть США 1</span><span class="sxs-lookup"><span data-stu-id="c77b2-158">East US 1</span></span> | <span data-ttu-id="c77b2-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="c77b2-159">191.238.6.43</span></span> | <span data-ttu-id="c77b2-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="c77b2-160">40.121.158.30</span></span> |
| <span data-ttu-id="c77b2-161">Восток США 2</span><span class="sxs-lookup"><span data-stu-id="c77b2-161">East US 2</span></span> | <span data-ttu-id="c77b2-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="c77b2-162">191.239.224.107</span></span> | <span data-ttu-id="c77b2-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="c77b2-163">40.79.84.180</span></span> |
| <span data-ttu-id="c77b2-164">Центральная Индия</span><span class="sxs-lookup"><span data-stu-id="c77b2-164">India Central</span></span> | <span data-ttu-id="c77b2-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="c77b2-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="c77b2-166">Южная Индия</span><span class="sxs-lookup"><span data-stu-id="c77b2-166">India South</span></span> | <span data-ttu-id="c77b2-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="c77b2-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="c77b2-168">Западная Индия</span><span class="sxs-lookup"><span data-stu-id="c77b2-168">India West</span></span> | <span data-ttu-id="c77b2-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="c77b2-169">104.211.160.80</span></span> | |
| <span data-ttu-id="c77b2-170">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="c77b2-170">Japan East</span></span> | <span data-ttu-id="c77b2-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="c77b2-171">191.237.240.43</span></span> | <span data-ttu-id="c77b2-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="c77b2-172">13.78.61.196</span></span> |
| <span data-ttu-id="c77b2-173">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="c77b2-173">Japan West</span></span> | <span data-ttu-id="c77b2-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="c77b2-174">191.238.68.11</span></span> | <span data-ttu-id="c77b2-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="c77b2-175">104.214.148.156</span></span> |
| <span data-ttu-id="c77b2-176">Центральная Корея</span><span class="sxs-lookup"><span data-stu-id="c77b2-176">Korea Central</span></span> | <span data-ttu-id="c77b2-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="c77b2-177">52.231.32.42</span></span> | |
| <span data-ttu-id="c77b2-178">Южная Корея</span><span class="sxs-lookup"><span data-stu-id="c77b2-178">Korea South</span></span> | <span data-ttu-id="c77b2-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="c77b2-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="c77b2-180">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="c77b2-180">North Central US</span></span> | <span data-ttu-id="c77b2-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="c77b2-181">23.98.55.75</span></span> | <span data-ttu-id="c77b2-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="c77b2-182">23.96.178.199</span></span> |
| <span data-ttu-id="c77b2-183">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="c77b2-183">North Europe</span></span> | <span data-ttu-id="c77b2-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="c77b2-184">191.235.193.75</span></span> | <span data-ttu-id="c77b2-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="c77b2-185">40.113.93.91</span></span> |
| <span data-ttu-id="c77b2-186">Южно-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="c77b2-186">South Central US</span></span> | <span data-ttu-id="c77b2-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="c77b2-187">23.98.162.75</span></span> | <span data-ttu-id="c77b2-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="c77b2-188">13.66.62.124</span></span> |
| <span data-ttu-id="c77b2-189">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="c77b2-189">South East Asia</span></span> | <span data-ttu-id="c77b2-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="c77b2-190">23.100.117.95</span></span> | <span data-ttu-id="c77b2-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="c77b2-191">104.43.15.0</span></span> |
| <span data-ttu-id="c77b2-192">Север Соединенного Королевства</span><span class="sxs-lookup"><span data-stu-id="c77b2-192">UK North</span></span> | <span data-ttu-id="c77b2-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="c77b2-193">13.87.97.210</span></span> | |
| <span data-ttu-id="c77b2-194">Южная часть Соединенного Королевства 1</span><span class="sxs-lookup"><span data-stu-id="c77b2-194">UK South 1</span></span> | <span data-ttu-id="c77b2-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="c77b2-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="c77b2-196">Юг Соединенного Королевства 2</span><span class="sxs-lookup"><span data-stu-id="c77b2-196">UK South 2</span></span> | <span data-ttu-id="c77b2-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="c77b2-197">13.87.34.7</span></span> | |
| <span data-ttu-id="c77b2-198">Западная часть Великобритании</span><span class="sxs-lookup"><span data-stu-id="c77b2-198">UK West</span></span> | <span data-ttu-id="c77b2-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="c77b2-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="c77b2-200">Западно-центральная часть США</span><span class="sxs-lookup"><span data-stu-id="c77b2-200">West Central US</span></span> | <span data-ttu-id="c77b2-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="c77b2-201">13.78.145.25</span></span> | |
| <span data-ttu-id="c77b2-202">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="c77b2-202">West Europe</span></span> | <span data-ttu-id="c77b2-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="c77b2-203">191.237.232.75</span></span> | <span data-ttu-id="c77b2-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="c77b2-204">40.68.37.158</span></span> |
| <span data-ttu-id="c77b2-205">Западная часть США 1</span><span class="sxs-lookup"><span data-stu-id="c77b2-205">West US 1</span></span> | <span data-ttu-id="c77b2-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="c77b2-206">23.99.34.75</span></span> | <span data-ttu-id="c77b2-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="c77b2-207">104.42.238.205</span></span> |
| <span data-ttu-id="c77b2-208">Западный регион США 2</span><span class="sxs-lookup"><span data-stu-id="c77b2-208">West US 2</span></span> | <span data-ttu-id="c77b2-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="c77b2-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="c77b2-210">Изменение политики подключения для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c77b2-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="c77b2-211">Чтобы изменить политику подключения базы данных SQL Azure для сервера базы данных SQL Azure, используйте [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="c77b2-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="c77b2-212">Если задана политика подключения **Прокси-сервер**, то всех сетевые пакеты проходят через шлюз базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="c77b2-213">Для этого режима необходимо разрешить исходящий трафик только через IP-адрес шлюза базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b2-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="c77b2-214">В режиме **Прокси-сервер** задержка выше, чем в режиме **Перенаправление**.</span><span class="sxs-lookup"><span data-stu-id="c77b2-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="c77b2-215">Если используется политика подключения **Перенаправление**, то все сетевые пакеты передаются непосредственно в ПО промежуточного уровня прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c77b2-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="c77b2-216">Для этого режима необходимо разрешить исходящий трафик для нескольких IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c77b2-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="c77b2-217">Сценарий для изменения параметров подключения</span><span class="sxs-lookup"><span data-stu-id="c77b2-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c77b2-218">Для работы этого сценария требуется [модуль Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c77b2-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="c77b2-219">Приведенный ниже сценарий PowerShell показывает, как изменить политику подключения.</span><span class="sxs-lookup"><span data-stu-id="c77b2-219">The following PowerShell script shows how to change the connection policy.</span></span>

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

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="c77b2-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c77b2-220">Next steps</span></span>

- <span data-ttu-id="c77b2-221">Сведения о том, как изменить политику подключения базы данных SQL Azure для сервера базы данных SQL Azure, см. в разделе [Create or Update Server Connection Policy](https://msdn.microsoft.com/library/azure/mt604439.aspx) (Создание или изменение политики подключения сервера).</span><span class="sxs-lookup"><span data-stu-id="c77b2-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="c77b2-222">Сведения о поведении подключения к базе данных SQL Azure клиентов, использующих ADO.NET 4.5 или более поздней версии, см. в разделе [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="c77b2-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="c77b2-223">Общая информация о разработке приложений приведена в разделе [Обзор разработки приложений баз данных SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c77b2-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
