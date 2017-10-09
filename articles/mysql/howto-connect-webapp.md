---
title: "aaaConnect существующей службы приложений Azure tooAzure базы данных MySQL | Документы Microsoft"
description: "Инструкции о том, как tooproperly подключаться существующей службы приложений Azure tooAzure базы данных для MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="9edd8-103">Подключение к MySQL server существующей службы приложений Azure tooAzure базы данных</span><span class="sxs-lookup"><span data-stu-id="9edd8-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="9edd8-104">В этом документе объясняется, как tooconnect существующей службы приложений Azure tooyour базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9edd8-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9edd8-105">Before you begin</span></span>
<span data-ttu-id="9edd8-106">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9edd8-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9edd8-107">Создайте базу данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="9edd8-108">Дополнительные сведения приведены слишком[как toocreate базы данных Azure для сервера MySQL с портала](quickstart-create-mysql-server-database-using-azure-portal.md) или [как toocreate базы данных Azure для MySQL server, используя интерфейс командной строки](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9edd8-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="9edd8-109">В настоящее время существует два tooenable доступа решений, службе приложений Azure tooan базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="9edd8-110">Оба решения включают настройку правил брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="9edd8-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="9edd8-111">Решение 1 - создать правило брандмауэра tooallow все IP-адреса</span><span class="sxs-lookup"><span data-stu-id="9edd8-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="9edd8-112">База данных Azure для MySQL обеспечивает управление доступом с помощью tooprotect брандмауэра данных.</span><span class="sxs-lookup"><span data-stu-id="9edd8-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="9edd8-113">При подключении из службы приложений Azure tooAzure базы данных для сервера MySQL следует помнить, что hello исходящих IP-адреса службы приложений являются динамическими по своей природе.</span><span class="sxs-lookup"><span data-stu-id="9edd8-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="9edd8-114">доступность hello tooensure службе приложений Azure, мы рекомендуем использовать это решение tooallow все IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9edd8-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="9edd8-115">Корпорация Майкрософт работает для долгосрочного tooavoid решения, позволяя все IP-адреса для служб Azure tooconnect tooAzure базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="9edd8-116">В колонке сервера MySQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке hello базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="9edd8-118">Введите значения в полях **ИМЯ ПРАВИЛА**, **НАЧАЛЬНЫЙ IP-АДРЕС** и **КОНЕЧНЫЙ IP-АДРЕС**.</span><span class="sxs-lookup"><span data-stu-id="9edd8-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="9edd8-119">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9edd8-119">Then click **Save**.</span></span>
   - <span data-ttu-id="9edd8-120">Имя правила: Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="9edd8-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="9edd8-121">Начальный IP-адрес: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="9edd8-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="9edd8-122">Конечный IP-адрес: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="9edd8-122">End IP: 255.255.255.255</span></span>

   ![Портал Azure — добавление всех IP-адресов](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="9edd8-124">Решение 2 - создать брандмауэр tooexplicitly правила Разрешить исходящие IP-адресов</span><span class="sxs-lookup"><span data-stu-id="9edd8-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="9edd8-125">Можно явно добавить, что все hello исходящий IP-адреса службы приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="9edd8-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="9edd8-126">В колонке hello свойства приложения службы, откройте ваш **ИСХОДЯЩИЙ IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="9edd8-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Портал Azure — просмотр исходящих IP-адресов](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="9edd8-128">В колонке безопасности подключение к MySQL hello добавьте исходящий IP-адресов по одному.</span><span class="sxs-lookup"><span data-stu-id="9edd8-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Портал Azure — добавление явных IP-адресов](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="9edd8-130">Помните, слишком**Сохранить** правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="9edd8-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="9edd8-131">Хотя hello службы приложений Azure пытается tookeep IP адресов константа со временем, существуют случаи, где hello IP-адреса могут измениться.</span><span class="sxs-lookup"><span data-stu-id="9edd8-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="9edd8-132">Например, когда hello перезапускает приложение возникает, операции масштабирования, или при добавлении новых компьютеров в данных Azure региональные центры tooincrease hello емкости.</span><span class="sxs-lookup"><span data-stu-id="9edd8-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="9edd8-133">При изменения hello IP-адресов, приложение hello может простаивать в событии hello, больше не может подключиться toohello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="9edd8-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="9edd8-134">При выборе одной из предыдущих решения hello, рассмотрите возможность этой возможности.</span><span class="sxs-lookup"><span data-stu-id="9edd8-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="9edd8-135">Настройка SSL</span><span class="sxs-lookup"><span data-stu-id="9edd8-135">SSL configuration</span></span>
<span data-ttu-id="9edd8-136">Протокол SSL по умолчанию включен для базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="9edd8-137">Если приложение не использует SSL tooconnect toohello, базы данных, то необходимо toodisable SSL на сервер MySQL.</span><span class="sxs-lookup"><span data-stu-id="9edd8-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="9edd8-138">Дополнительные сведения о том, как tooconfigure SSL, см. в разделе [использование SSL с базой данных Azure для MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9edd8-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9edd8-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9edd8-139">Next steps</span></span>
<span data-ttu-id="9edd8-140">Дополнительные сведения о строках соединения см. в разделе слишком[строки подключения](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="9edd8-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
