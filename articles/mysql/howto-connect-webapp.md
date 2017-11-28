---
title: "Подключение существующей службы приложений Azure к базе данных Azure для MySQL | Документы Майкрософт"
description: "Инструкции по правильному подключению существующей службы приложений Azure к базе данных Azure для MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="7a7e2-103">Подключение существующей службы приложений Azure к базе данных Azure для сервера MySQL</span><span class="sxs-lookup"><span data-stu-id="7a7e2-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="7a7e2-104">В этом документе объясняется, как подключить существующую службу приложений Azure к базе данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7a7e2-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7a7e2-105">Before you begin</span></span>
<span data-ttu-id="7a7e2-106">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a7e2-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7a7e2-107">Создайте базу данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="7a7e2-108">Дополнительные сведения см. в статье [Создание базы данных Azure для сервера MySQL с помощью портала Azure](quickstart-create-mysql-server-database-using-azure-portal.md) или [Создание сервера базы данных Azure для MySQL с помощью Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7a7e2-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="7a7e2-109">В настоящее время существует два решения предоставления доступа из службы приложений Azure к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="7a7e2-110">Оба решения включают настройку правил брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="7a7e2-111">Решение 1. Создание правила брандмауэра, разрешающего все IP-адреса</span><span class="sxs-lookup"><span data-stu-id="7a7e2-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="7a7e2-112">База данных Azure для MySQL обеспечивает безопасность доступа, используя брандмауэр для защиты данных.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="7a7e2-113">При настройке подключения из службы приложений Azure к базе данных Azure для сервера MySQL имейте в виду, что исходящие IP-адреса службы приложений являются динамическими по своей природе.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="7a7e2-114">Чтобы обеспечить доступность службы приложений Azure, рекомендуется выбрать это решение, разрешив ВСЕ IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7e2-115">Специалисты Майкрософт находятся в поиске долгосрочного решения, которое позволит отказаться от разрешения всех IP-адресов, предоставляя доступ службы приложений Azure к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="7a7e2-116">В колонке сервера MySQL в разделе "Параметры" щелкните **Безопасность подключения**, чтобы открыть колонку "Безопасность подключения" базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="7a7e2-118">Введите значения в полях **ИМЯ ПРАВИЛА**, **НАЧАЛЬНЫЙ IP-АДРЕС** и **КОНЕЧНЫЙ IP-АДРЕС**.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="7a7e2-119">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-119">Then click **Save**.</span></span>
   - <span data-ttu-id="7a7e2-120">Имя правила: Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="7a7e2-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="7a7e2-121">Начальный IP-адрес: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="7a7e2-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="7a7e2-122">Конечный IP-адрес: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="7a7e2-122">End IP: 255.255.255.255</span></span>

   ![Портал Azure — добавление всех IP-адресов](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="7a7e2-124">Решение 2. Создание правила брандмауэра, явно разрешающего исходящие IP-адреса</span><span class="sxs-lookup"><span data-stu-id="7a7e2-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="7a7e2-125">Вы можете явно добавить все исходящие IP-адреса службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="7a7e2-126">В колонке "Свойства службы приложений" обратите внимание на поле **ИСХОДЯЩИЙ IP-АДРЕС**.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Портал Azure — просмотр исходящих IP-адресов](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="7a7e2-128">В колонке "Безопасность подключения" для MySQL добавьте исходящие IP-адреса по одному.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Портал Azure — добавление явных IP-адресов](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="7a7e2-130">Не забывайте **сохранять** правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="7a7e2-131">Хотя служба приложений Azure пытается поддерживать постоянные IP-адреса, бывают случаи, когда IP-адреса могут измениться.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="7a7e2-132">Например, это происходит, когда приложение выполняет очистку или возникает операция масштабирования, а также при добавлении новых виртуальных машин в региональные центры обработки данных Azure для повышения емкости.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="7a7e2-133">При изменении IP-адресов может наблюдаться простой приложения, если оно больше не может подключиться к серверу MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="7a7e2-134">Учтите эту вероятность при выборе решения.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="7a7e2-135">Настройка SSL</span><span class="sxs-lookup"><span data-stu-id="7a7e2-135">SSL configuration</span></span>
<span data-ttu-id="7a7e2-136">Протокол SSL по умолчанию включен для базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="7a7e2-137">Если приложение не использует SSL для подключения к базе данных, необходимо отключить SSL для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="7a7e2-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="7a7e2-138">Дополнительные сведения о настройке SSL см. в статье, посвященной [использованию SSL-подключений с базой данных Azure для MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="7a7e2-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a7e2-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a7e2-139">Next steps</span></span>
<span data-ttu-id="7a7e2-140">Дополнительные сведения о строках подключения см. в [соответствующей статье](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="7a7e2-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
