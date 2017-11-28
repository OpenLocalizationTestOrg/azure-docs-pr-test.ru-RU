---
title: "Первый Azure базы данных для базы данных MySQL - Azure CLI aaaDesign | Документы Microsoft"
description: "В этом учебнике описано как toocreate и управления базой данных Azure для MySQL server и базы данных с помощью Azure CLI 2.0 из командной строки hello."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="37208-103">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="37208-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="37208-104">База данных Azure для MySQL — это служба реляционной базы данных в зависимости от базы данных MySQL Community Edition Microsoft cloud hello.</span><span class="sxs-lookup"><span data-stu-id="37208-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="37208-105">В этом учебнике используется Azure CLI (интерфейс командной строки) и другие служебные программы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="37208-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="37208-106">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="37208-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="37208-107">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="37208-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="37208-108">Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate базы данных</span><span class="sxs-lookup"><span data-stu-id="37208-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="37208-109">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="37208-109">Load sample data</span></span>
> * <span data-ttu-id="37208-110">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="37208-110">Query data</span></span>
> * <span data-ttu-id="37208-111">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="37208-111">Update data</span></span>
> * <span data-ttu-id="37208-112">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="37208-112">Restore data</span></span>

<span data-ttu-id="37208-113">Вы можете использовать hello оболочки облако Azure в обозревателе hello, или [установить CLI Azure 2.0]( /cli/azure/install-azure-cli) на блоки собственного компьютера toorun hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="37208-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="37208-114">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="37208-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="37208-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="37208-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="37208-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37208-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="37208-117">Если у вас несколько подписок, выберите нужную подписку hello, в котором hello ресурсов существует, или плата за.</span><span class="sxs-lookup"><span data-stu-id="37208-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="37208-118">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="37208-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="37208-119">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="37208-119">Create a resource group</span></span>
<span data-ttu-id="37208-120">Создайте [группу ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview), выполнив команду [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="37208-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="37208-121">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="37208-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="37208-122">Hello следующий пример создает группу ресурсов с именем `mycliresource` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="37208-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="37208-123">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="37208-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="37208-124">Можно создайте базу данных Azure для сервера MySQL с помощью сервера mysql az hello создать команду.</span><span class="sxs-lookup"><span data-stu-id="37208-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="37208-125">Сервер может управлять несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="37208-125">A server can manage multiple databases.</span></span> <span data-ttu-id="37208-126">Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.</span><span class="sxs-lookup"><span data-stu-id="37208-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="37208-127">Hello следующий пример создает базы данных Azure для MySQL server, расположенный в `westus` в группе ресурсов hello `mycliresource` с именем `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="37208-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="37208-128">Hello сервер имеет журнал администратора в с именем `myadmin` и пароль `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="37208-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="37208-129">сервер Hello создается с **основные** уровня производительности и **50** единиц, общим для всех баз данных hello в hello server вычислительных операций.</span><span class="sxs-lookup"><span data-stu-id="37208-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="37208-130">Вычислений и хранилища можно масштабировать вверх или вниз в зависимости от потребностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="37208-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="37208-131">Настройка правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="37208-131">Configure firewall rule</span></span>
<span data-ttu-id="37208-132">Можно создайте базу данных Azure для правила брандмауэра уровня сервера MySQL с hello az mysql правила брандмауэра для сервера — команда «Создать».</span><span class="sxs-lookup"><span data-stu-id="37208-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="37208-133">Правила брандмауэра уровня сервера позволяет внешнего приложения, такие как **mysql** средство командной строки или MySQL Workbench tooconnect tooyour server через брандмауэр службы MySQL в Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37208-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="37208-134">Hello следующий пример создает правило брандмауэра для предопределенный адрес диапазона.</span><span class="sxs-lookup"><span data-stu-id="37208-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="37208-135">Этот пример hello все возможные диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="37208-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="37208-136">Получить сведения о соединении hello</span><span class="sxs-lookup"><span data-stu-id="37208-136">Get hello connection information</span></span>

<span data-ttu-id="37208-137">tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.</span><span class="sxs-lookup"><span data-stu-id="37208-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="37208-138">Hello получается в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="37208-138">hello result is in JSON format.</span></span> <span data-ttu-id="37208-139">Запишите hello **fullyQualifiedDomainName** и **Имя_входа_администратора**.</span><span class="sxs-lookup"><span data-stu-id="37208-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="37208-140">Подключиться с помощью mysql server toohello</span><span class="sxs-lookup"><span data-stu-id="37208-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="37208-141">Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour подключения базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="37208-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="37208-142">В этом примере команда hello имеет вид:</span><span class="sxs-lookup"><span data-stu-id="37208-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="37208-143">Создание пустой базы данных</span><span class="sxs-lookup"><span data-stu-id="37208-143">Create a blank database</span></span>
<span data-ttu-id="37208-144">Когда вы будете toohello подключенного сервера, создайте пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="37208-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="37208-145">В строке приветствия выполните hello, выполнив команду подключения hello tooswitch toothis вновь созданные базы данных:</span><span class="sxs-lookup"><span data-stu-id="37208-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="37208-146">Создание таблиц в базе данных hello</span><span class="sxs-lookup"><span data-stu-id="37208-146">Create tables in hello database</span></span>
<span data-ttu-id="37208-147">Теперь, когда вы знаете, как tooconnect toohello базы данных Azure для базы данных MySQL, мы можем открыть как toocomplete некоторых базовых задач.</span><span class="sxs-lookup"><span data-stu-id="37208-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="37208-148">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="37208-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="37208-149">Давайте создадим таблицу, в которой хранятся данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="37208-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="37208-150">Загрузка данных в таблицы hello</span><span class="sxs-lookup"><span data-stu-id="37208-150">Load data into hello tables</span></span>
<span data-ttu-id="37208-151">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="37208-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="37208-152">Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных.</span><span class="sxs-lookup"><span data-stu-id="37208-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="37208-153">Теперь у вас две строки образца данных в таблицу hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="37208-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="37208-154">Запрашивать и обновлять данные hello в таблицах hello</span><span class="sxs-lookup"><span data-stu-id="37208-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="37208-155">Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="37208-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="37208-156">Можно также обновить данные hello в таблицах hello.</span><span class="sxs-lookup"><span data-stu-id="37208-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="37208-157">Строка Hello обновляется соответствующим образом при извлечении данных.</span><span class="sxs-lookup"><span data-stu-id="37208-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="37208-158">Восстановление предыдущей точки tooa базы данных времени</span><span class="sxs-lookup"><span data-stu-id="37208-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="37208-159">Представьте, что вы случайно удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="37208-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="37208-160">Восстановить ее будет не просто.</span><span class="sxs-lookup"><span data-stu-id="37208-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="37208-161">Базы данных Azure для MySQL дает точки назад tooany toogo времени в hello последнего вверх too35 дни и в новом сервере tooa времени этой точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="37208-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="37208-162">Можно использовать этот новый сервер toorecover удаленные данные.</span><span class="sxs-lookup"><span data-stu-id="37208-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="37208-163">Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.</span><span class="sxs-lookup"><span data-stu-id="37208-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="37208-164">Для восстановления hello требуется hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="37208-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="37208-165">Точка восстановления: выберите в момент, выполняемой до hello сервер был изменен.</span><span class="sxs-lookup"><span data-stu-id="37208-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="37208-166">Должен быть больше или равен старые резервного копирования значение toohello базы данных-источника.</span><span class="sxs-lookup"><span data-stu-id="37208-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="37208-167">Целевой сервер: Введите имя нового сервера требуется toorestore для</span><span class="sxs-lookup"><span data-stu-id="37208-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="37208-168">Исходный сервер: укажите имя hello hello сервера, toorestore из</span><span class="sxs-lookup"><span data-stu-id="37208-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="37208-169">Расположение: Не удается выбрать область hello, по умолчанию это то же, что hello исходного сервера</span><span class="sxs-lookup"><span data-stu-id="37208-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="37208-170">сервер toorestore hello и [восстановить tooa в момент](./howto-restore-server-portal.md) перед hello таблица была удалена.</span><span class="sxs-lookup"><span data-stu-id="37208-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="37208-171">Восстановление сервера tooa другой момент времени, создает повторяющиеся новый сервер как исходный сервер hello как hello моменту времени можно указать, при условии, что он находится в пределах срока хранения hello вашей [уровня службы](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="37208-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="37208-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37208-172">Next Steps</span></span>
<span data-ttu-id="37208-173">Из этого руководства вы узнали, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="37208-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="37208-174">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="37208-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="37208-175">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="37208-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="37208-176">Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate базы данных</span><span class="sxs-lookup"><span data-stu-id="37208-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="37208-177">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="37208-177">Load sample data</span></span>
> * <span data-ttu-id="37208-178">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="37208-178">Query data</span></span>
> * <span data-ttu-id="37208-179">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="37208-179">Update data</span></span>
> * <span data-ttu-id="37208-180">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="37208-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37208-181">Примеры Azure CLI для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="37208-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
