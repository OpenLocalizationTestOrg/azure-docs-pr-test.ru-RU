---
title: "aaaCreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью командной строки Azure CLI."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="8e261-103">Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e261-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="8e261-104">Правила брандмауэра уровня сервера включите tooan доступа toomanage администраторы базы данных Azure для сервера PostgreSQL определенный IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="8e261-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="8e261-105">Командами удобный Azure CLI можно создать, обновить, удалить, а также выполнять их список и Показать toomanage правила брандмауэра сервера.</span><span class="sxs-lookup"><span data-stu-id="8e261-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="8e261-106">Обзор брандмауэров базы данных Azure для PostgreSQL приведен в разделе [Правила брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8e261-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e261-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e261-107">Prerequisites</span></span>
<span data-ttu-id="8e261-108">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="8e261-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="8e261-109">[сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="8e261-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="8e261-110">Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.</span><span class="sxs-lookup"><span data-stu-id="8e261-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="8e261-111">Настройка правил брандмауэра сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8e261-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="8e261-112">Hello [az postgres правила брандмауэра для сервера —](/cli/azure/postgres/server/firewall-rule) команды, используемые tooconfigure правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="8e261-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="8e261-113">Вывод списка правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="8e261-113">List firewall rules</span></span> 
<span data-ttu-id="8e261-114">toolist hello существующих правил брандмауэра сервера на сервере hello запуска hello [список правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#list) команды.</span><span class="sxs-lookup"><span data-stu-id="8e261-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="8e261-115">выходные данные Hello перечислены правила hello, если таковая имеется, по умолчанию в формате JSON формата.</span><span class="sxs-lookup"><span data-stu-id="8e261-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="8e261-116">Можно использовать переключатель hello `--output table` для более удобочитаемый формат таблицы в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="8e261-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="8e261-117">Создание правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="8e261-117">Create firewall rule</span></span>
<span data-ttu-id="8e261-118">новое правило брандмауэра на сервере hello, выполните hello toocreate [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="8e261-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="8e261-119">В этом примере обеспечивает ряд все IP-адреса tooaccess hello сервера **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="8e261-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="8e261-120">tooallow единственном числе tooaccess IP адрес, укажите hello таким же адресом как hello начальный IP- и конечного IP-адресов, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="8e261-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="8e261-121">После успешного выполнения выходные данные команды hello указаны подробности hello hello правило брандмауэра, которое вы создали, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="8e261-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="8e261-122">В случае сбоя hello вместо вывода showserror текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="8e261-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="8e261-123">Обновление правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="8e261-123">Update firewall rule</span></span> 
<span data-ttu-id="8e261-124">Обновление существующего правила брандмауэра на сервере с помощью hello [обновление правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#update) команды.</span><span class="sxs-lookup"><span data-stu-id="8e261-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="8e261-125">Укажите имя hello существующее правило брандмауэра, как входные данные и hello начала IP-адресов и конечным IP атрибуты tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="8e261-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="8e261-126">При успешном завершении hello выходные данные команды выводятся сведения hello hello правила брандмауэра, которые были обновлены, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="8e261-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="8e261-127">В случае сбоя hello вместо вывода showserror текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="8e261-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="8e261-128">Если правило брандмауэра hello не существует, он возвращает созданный командой обновления hello.</span><span class="sxs-lookup"><span data-stu-id="8e261-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="8e261-129">Отображение сведений о правиле брандмауэра</span><span class="sxs-lookup"><span data-stu-id="8e261-129">Show firewall rule details</span></span>
<span data-ttu-id="8e261-130">Также можно показать существующий брандмауэра hello сведения о правиле, для сервера, запустив [Показать правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#show) команды.</span><span class="sxs-lookup"><span data-stu-id="8e261-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="8e261-131">После успешного выполнения выходные данные команды hello указаны подробности hello hello правило брандмауэра, которое вы задали, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="8e261-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="8e261-132">В случае сбоя hello вместо вывода showserror текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="8e261-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="8e261-133">Удаление правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="8e261-133">Delete firewall rule</span></span>
<span data-ttu-id="8e261-134">toorevoke доступ с сервера hello диапазона IP-удаление существующего правила брандмауэра, выполнив hello [az postgres правила брандмауэра для сервера — Удалить](/cli/azure/postgres/server/firewall-rule#delete) команды.</span><span class="sxs-lookup"><span data-stu-id="8e261-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="8e261-135">Укажите имя hello hello существующее правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="8e261-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="8e261-136">При успешном выполнении выходные данные отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="8e261-136">Upon success, there is no output.</span></span> <span data-ttu-id="8e261-137">При сбое возвращается сообщение об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="8e261-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e261-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e261-138">Next steps</span></span>
- <span data-ttu-id="8e261-139">Аналогичным образом, можно использовать веб-браузер слишком[Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8e261-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="8e261-140">Узнайте больше о [правилах брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8e261-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="8e261-141">Справку в подключении tooan базы данных Azure для сервера PostgreSQL см [библиотеки подключений к базе данных Azure для PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="8e261-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
