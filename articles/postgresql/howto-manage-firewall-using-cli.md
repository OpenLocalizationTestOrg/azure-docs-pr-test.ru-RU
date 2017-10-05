---
title: "Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI | Документация Майкрософт"
description: "В этой статье описывается, как создать базу данных Azure для правил брандмауэра PostgreSQL и управлять ею с помощью интерфейса командной строки Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="408e2-103">Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="408e2-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="408e2-104">Правила брандмауэра уровня сервера позволяют администраторам управлять доступом к серверу базы данных Azure для PostgreSQL с указанного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="408e2-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="408e2-105">С помощью удобных команд Azure CLI можно создавать, обновлять, удалять, выводить список и отображать правила брандмауэра для управления сервером.</span><span class="sxs-lookup"><span data-stu-id="408e2-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="408e2-106">Обзор брандмауэров базы данных Azure для PostgreSQL приведен в разделе [Правила брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="408e2-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="408e2-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="408e2-107">Prerequisites</span></span>
<span data-ttu-id="408e2-108">Прежде чем приступить к выполнению этого руководства, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="408e2-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="408e2-109">[сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="408e2-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="408e2-110">Установите служебную программу командной строки [Azure CLI 2.0](/cli/azure/install-azure-cli) или используйте Azure Cloud Shell в браузере.</span><span class="sxs-lookup"><span data-stu-id="408e2-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="408e2-111">Настройка правил брандмауэра сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="408e2-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="408e2-112">Команда [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) используется для настройки правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="408e2-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="408e2-113">Вывод списка правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="408e2-113">List firewall rules</span></span> 
<span data-ttu-id="408e2-114">Чтобы вывести список существующих правил брандмауэра сервера на сервере, запустите команду [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list).</span><span class="sxs-lookup"><span data-stu-id="408e2-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="408e2-115">Выходные данные будут содержать правила, если они имеются, в используемом по умолчанию формате JSON.</span><span class="sxs-lookup"><span data-stu-id="408e2-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="408e2-116">Вы можете использовать `--output table`, чтобы получить выходные данные в виде более удобной таблицы.</span><span class="sxs-lookup"><span data-stu-id="408e2-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="408e2-117">Создание правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="408e2-117">Create firewall rule</span></span>
<span data-ttu-id="408e2-118">Чтобы создать правило брандмауэра на сервере, выполните команду [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="408e2-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="408e2-119">Этот пример разрешает доступ к серверу **mypgserver-20170401.postgres.database.azure.com** всем диапазонам IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="408e2-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="408e2-120">Чтобы разрешить доступ с отдельного IP-адреса, укажите одинаковый начальный и конечный IP-адрес, как показано в этом примере.</span><span class="sxs-lookup"><span data-stu-id="408e2-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="408e2-121">При успешном выполнении команды ее выходные данные будут содержать сведения о созданном правиле брандмауэра в используемом по умолчанию формате JSON.</span><span class="sxs-lookup"><span data-stu-id="408e2-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="408e2-122">Если возникнет сбой, выходные данные будут содержать сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="408e2-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="408e2-123">Обновление правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="408e2-123">Update firewall rule</span></span> 
<span data-ttu-id="408e2-124">Обновите существующее правило брандмауэра на сервере с помощью команды [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update).</span><span class="sxs-lookup"><span data-stu-id="408e2-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="408e2-125">В качестве входных данных укажите имя существующего правила брандмауэра, которое нужно обновить, а также атрибуты начального и конечного IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="408e2-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="408e2-126">При успешном выполнении команды ее выходные данные будут содержать сведения об обновленном правиле брандмауэра в используемом по умолчанию формате JSON.</span><span class="sxs-lookup"><span data-stu-id="408e2-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="408e2-127">Если возникнет сбой, выходные данные будут содержать сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="408e2-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="408e2-128">Если правило брандмауэра не существует, оно будет создано командой update.</span><span class="sxs-lookup"><span data-stu-id="408e2-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="408e2-129">Отображение сведений о правиле брандмауэра</span><span class="sxs-lookup"><span data-stu-id="408e2-129">Show firewall rule details</span></span>
<span data-ttu-id="408e2-130">Вы также можете отобразить сведения о существующем правиле брандмауэра, выполнив команду [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show).</span><span class="sxs-lookup"><span data-stu-id="408e2-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="408e2-131">При успешном выполнении команды ее выходные данные будут содержать сведения об указанном правиле брандмауэра в используемом по умолчанию формате JSON.</span><span class="sxs-lookup"><span data-stu-id="408e2-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="408e2-132">Если возникнет сбой, выходные данные будут содержать сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="408e2-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="408e2-133">Удаление правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="408e2-133">Delete firewall rule</span></span>
<span data-ttu-id="408e2-134">Чтобы отменить доступ для диапазона IP-адресов с сервера, удалите существующее правило брандмауэра, выполнив команду [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete).</span><span class="sxs-lookup"><span data-stu-id="408e2-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="408e2-135">Укажите имя существующего правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="408e2-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="408e2-136">При успешном выполнении выходные данные отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="408e2-136">Upon success, there is no output.</span></span> <span data-ttu-id="408e2-137">В случае сбоя возвращается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="408e2-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="408e2-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="408e2-138">Next steps</span></span>
- <span data-ttu-id="408e2-139">Аналогичным образом можно использовать веб-браузер, чтобы [создать правила брандмауэра базы данных Azure для PostgreSQL и управлять ими с помощью портала Azure](howto-manage-firewall-using-portal.md).</span><span class="sxs-lookup"><span data-stu-id="408e2-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="408e2-140">Узнайте больше о [правилах брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="408e2-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="408e2-141">Справка по подключению к серверу базы данных Azure для PostgreSQL доступна в разделе [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="408e2-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
