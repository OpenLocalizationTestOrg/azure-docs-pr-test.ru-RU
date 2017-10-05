---
title: "Проектирование первой базы данных Azure для MySQL с помощью Azure CLI | Документация Майкрософт"
description: "Это руководство содержит сведения о создании базы данных и сервера базы данных Azure для MySQL и управлении ими с помощью Azure CLI 2.0 из командной строки."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="48fa4-103">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="48fa4-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="48fa4-104">База данных Azure для MySQL — это служба реляционной базы данных в Microsoft Cloud на основе ядра СУБД MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="48fa4-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="48fa4-105">Из этого руководства вы узнаете, как с помощью Azure CLI (интерфейса командной строки) и других служебных программ выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="48fa4-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48fa4-106">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="48fa4-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="48fa4-107">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="48fa4-107">Configure the server firewall</span></span>
> * <span data-ttu-id="48fa4-108">использование [средства командной строки MySQL](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="48fa4-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="48fa4-109">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-109">Load sample data</span></span>
> * <span data-ttu-id="48fa4-110">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-110">Query data</span></span>
> * <span data-ttu-id="48fa4-111">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-111">Update data</span></span>
> * <span data-ttu-id="48fa4-112">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-112">Restore data</span></span>

<span data-ttu-id="48fa4-113">Вы можете использовать Azure Cloud Shell в браузере или [установить Azure CLI 2.0]( /cli/azure/install-azure-cli) на компьютере, чтобы запустить блоки кода в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="48fa4-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48fa4-114">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="48fa4-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48fa4-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="48fa4-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="48fa4-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48fa4-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="48fa4-117">Если вы используете несколько подписок, выберите соответствующую подписку, в которой находится ресурс либо в которой за него взимается плата.</span><span class="sxs-lookup"><span data-stu-id="48fa4-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="48fa4-118">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="48fa4-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="48fa4-119">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="48fa4-119">Create a resource group</span></span>
<span data-ttu-id="48fa4-120">Создайте [группу ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview), выполнив команду [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="48fa4-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="48fa4-121">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="48fa4-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="48fa4-122">В следующем примере создается группа ресурсов с именем `mycliresource` в расположении `westus`.</span><span class="sxs-lookup"><span data-stu-id="48fa4-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="48fa4-123">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="48fa4-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="48fa4-124">Создайте сервер базы данных Azure для MySQL, выполнив команду az mysql server create.</span><span class="sxs-lookup"><span data-stu-id="48fa4-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="48fa4-125">Сервер может управлять несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-125">A server can manage multiple databases.</span></span> <span data-ttu-id="48fa4-126">Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="48fa4-127">В следующем примере в группе ресурсов `mycliresource` создается сервер базы данных Azure для MySQL с именем `mycliserver`, который расположен в `westus`.</span><span class="sxs-lookup"><span data-stu-id="48fa4-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="48fa4-128">Для сервера указано имя администратора для входа `myadmin` и пароль `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="48fa4-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="48fa4-129">Он создается с уровнем производительности **Базовый** и **50** единицами вычислений, которые совместно используются всеми базами данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="48fa4-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="48fa4-130">В зависимости от потребностей приложения можно увеличить или уменьшить масштаб вычислительных ресурсов и ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="48fa4-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="48fa4-131">Настройка правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="48fa4-131">Configure firewall rule</span></span>
<span data-ttu-id="48fa4-132">Создайте правило брандмауэра на уровне сервера базы данных Azure для MySQL, выполнив команду az mysql server firewall-rule create.</span><span class="sxs-lookup"><span data-stu-id="48fa4-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="48fa4-133">Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как средство командной строки **MySQL** или MySQL Workbench, подключаться к серверу через брандмауэр службы Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="48fa4-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="48fa4-134">В примере ниже показано создание правила брандмауэра для предопределенного диапазона адресов,</span><span class="sxs-lookup"><span data-stu-id="48fa4-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="48fa4-135">который в этом примере представляет наиболее полный диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="48fa4-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="48fa4-136">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="48fa4-136">Get the connection information</span></span>

<span data-ttu-id="48fa4-137">Чтобы подключиться к серверу, необходимо указать сведения об узле и учетные данные для доступа.</span><span class="sxs-lookup"><span data-stu-id="48fa4-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="48fa4-138">Результаты выводятся в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="48fa4-138">The result is in JSON format.</span></span> <span data-ttu-id="48fa4-139">Запишите значения **fullyQualifiedDomainName** и **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="48fa4-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="48fa4-140">Подключение к серверу с помощью MySQL</span><span class="sxs-lookup"><span data-stu-id="48fa4-140">Connect to the server using mysql</span></span>
<span data-ttu-id="48fa4-141">Используйте [средство командной строки MySQL](https://dev.mysql.com/doc/refman/5.6/en/mysql.html), чтобы установить соединение с сервером базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="48fa4-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="48fa4-142">В этом примере используется следующая команда:</span><span class="sxs-lookup"><span data-stu-id="48fa4-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="48fa4-143">Создание пустой базы данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-143">Create a blank database</span></span>
<span data-ttu-id="48fa4-144">Подключившись к серверу, создайте пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="48fa4-145">Выполните следующую команду в командной строке, чтобы подключиться к созданной базе данных:</span><span class="sxs-lookup"><span data-stu-id="48fa4-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="48fa4-146">Создание таблиц в базе данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-146">Create tables in the database</span></span>
<span data-ttu-id="48fa4-147">Теперь, когда вы знаете, как подключиться к базе данных Azure для MySQL, рассмотрим, как выполнить некоторые основные задачи.</span><span class="sxs-lookup"><span data-stu-id="48fa4-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="48fa4-148">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="48fa4-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="48fa4-149">Давайте создадим таблицу, в которой хранятся данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="48fa4-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="48fa4-150">Загрузка данных в таблицу</span><span class="sxs-lookup"><span data-stu-id="48fa4-150">Load data into the tables</span></span>
<span data-ttu-id="48fa4-151">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="48fa4-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="48fa4-152">Чтобы вставить некоторые строки данных, в открытом окне командной строки выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="48fa4-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="48fa4-153">Итак, в созданной ранее таблице содержится две строки данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="48fa4-154">Запрос и обновление данных в таблицах</span><span class="sxs-lookup"><span data-stu-id="48fa4-154">Query and update the data in the tables</span></span>
<span data-ttu-id="48fa4-155">Чтобы извлечь сведения из таблицы базы данных, выполните приведенный ниже запрос.</span><span class="sxs-lookup"><span data-stu-id="48fa4-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="48fa4-156">Вы можете также обновить данные в таблицах, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="48fa4-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="48fa4-157">При извлечении данных строка будет обновляться соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="48fa4-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="48fa4-158">Восстановление базы данных до предыдущей точки во времени</span><span class="sxs-lookup"><span data-stu-id="48fa4-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="48fa4-159">Представьте, что вы случайно удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="48fa4-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="48fa4-160">Восстановить ее будет не просто.</span><span class="sxs-lookup"><span data-stu-id="48fa4-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="48fa4-161">База данных Azure для MySQL позволяет вернуться в любой момент времени в течение последних 35 дней и восстановить данные на определенный момент времени на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="48fa4-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="48fa4-162">Вы можете восстановить удаленные данные с помощью нового сервера.</span><span class="sxs-lookup"><span data-stu-id="48fa4-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="48fa4-163">Указанные ниже шаги позволяют восстановить сервер до точки во времени, когда была создана таблица.</span><span class="sxs-lookup"><span data-stu-id="48fa4-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="48fa4-164">Чтобы восстановить данные, вам потребуются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="48fa4-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="48fa4-165">Точка восстановления. Выберите время до того момента, когда был изменен сервер.</span><span class="sxs-lookup"><span data-stu-id="48fa4-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="48fa4-166">Значение точки восстановления должно быть не меньше значения самой старой резервной копии исходной базы данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="48fa4-167">Целевой сервер. Укажите новое имя сервера, который нужно восстановить.</span><span class="sxs-lookup"><span data-stu-id="48fa4-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="48fa4-168">Исходный сервер. Укажите имя сервера, из которого требуется выполнить восстановление.</span><span class="sxs-lookup"><span data-stu-id="48fa4-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="48fa4-169">Расположение. Вы не сможете выбрать регион, по умолчанию он совпадает с исходным сервером.</span><span class="sxs-lookup"><span data-stu-id="48fa4-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="48fa4-170">Выполните предыдущую команду и восстановите сервер до [точки во времени](./howto-restore-server-portal.md) перед удалением таблицы.</span><span class="sxs-lookup"><span data-stu-id="48fa4-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="48fa4-171">Восстановление сервера до точки во времени создает копию сервера, где расположен исходный сервер, с состоянием на момент указанной точки во времени (в пределах срока хранения, установленного для вашего [уровня служб](./concepts-service-tiers.md)).</span><span class="sxs-lookup"><span data-stu-id="48fa4-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48fa4-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48fa4-172">Next Steps</span></span>
<span data-ttu-id="48fa4-173">Из этого руководства вы узнали, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="48fa4-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="48fa4-174">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="48fa4-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="48fa4-175">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="48fa4-175">Configure the server firewall</span></span>
> * <span data-ttu-id="48fa4-176">использование [средства командной строки MySQL](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="48fa4-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="48fa4-177">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-177">Load sample data</span></span>
> * <span data-ttu-id="48fa4-178">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-178">Query data</span></span>
> * <span data-ttu-id="48fa4-179">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="48fa4-179">Update data</span></span>
> * <span data-ttu-id="48fa4-180">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="48fa4-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48fa4-181">Примеры Azure CLI для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="48fa4-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
