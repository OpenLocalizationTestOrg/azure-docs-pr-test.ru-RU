---
title: "Azure CLI: создание базы данных SQL | Документация Майкрософт"
description: "Узнайте, как создать логический сервер базы данных SQL, правила брандмауэра на уровне сервера и базы данных с помощью Azure CLI."
keywords: "руководство по базам данных SQL, создание базы данных SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="d8a2f-104">Создание отдельной базы данных SQL Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d8a2f-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="d8a2f-105">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d8a2f-106">В этом руководстве подробно объясняется, как с помощью Azure CLI развернуть базу данных SQL Azure в [группе ресурсов Azure](../azure-resource-manager/resource-group-overview.md) на [логическом сервере базы данных Azure SQL](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="d8a2f-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d8a2f-108">Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве потребуется Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d8a2f-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d8a2f-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="d8a2f-111">Определение переменных</span><span class="sxs-lookup"><span data-stu-id="d8a2f-111">Define variables</span></span>

<span data-ttu-id="d8a2f-112">Определите переменные для использования в скриптах этого руководства.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d8a2f-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d8a2f-113">Create a resource group</span></span>

<span data-ttu-id="d8a2f-114">Создайте [группу ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d8a2f-115">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d8a2f-116">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="d8a2f-117">Создание логического сервера</span><span class="sxs-lookup"><span data-stu-id="d8a2f-117">Create a logical server</span></span>

<span data-ttu-id="d8a2f-118">Создайте [логический сервер базы данных SQL Azure ](sql-database-features.md) с помощью команды [az sql server create](/cli/azure/sql/server#create).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="d8a2f-119">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="d8a2f-120">В примере ниже показано создание сервера со случайным именем в группе ресурсов с именем администратора `ServerAdmin` и паролем `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="d8a2f-121">Замените эти предопределенные значения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="d8a2f-122">Настройка правил брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="d8a2f-122">Configure a server firewall rule</span></span>

<span data-ttu-id="d8a2f-123">Создайте [правило брандмауэра на уровне сервера базы данных Azure SQL](sql-database-firewall-configure.md) с помощью команды [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d8a2f-124">Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как SQL Server Management Studio или программе sqlcmd, подключаться к базе данных SQL через брандмауэр службы базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="d8a2f-125">В следующем примере брандмауэр открыт только для других ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="d8a2f-126">Чтобы включить возможность внешнего подключения, измените IP-адрес на соответствующий адрес своей среды.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="d8a2f-127">Чтобы открыть все IP-адреса, используйте 0.0.0.0 как начальный IP-адрес, а 255.255.255.255 — как конечный.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="d8a2f-128">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d8a2f-129">Если вы пытаетесь подключиться из корпоративной сети, исходящий трафик через порт 1433 может быть запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d8a2f-130">В таком случае вы не сможете подключиться к серверу базы данных SQL Azure. Для этого ваш ИТ-отдел должен открыть порт 1433.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="d8a2f-131">Создание базы данных на сервере с образцами данных</span><span class="sxs-lookup"><span data-stu-id="d8a2f-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="d8a2f-132">Создайте на сервере базу данных с [уровнем производительности S0](sql-database-service-tiers.md) с помощью команды [az sql db create](/cli/azure/sql/db#create).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="d8a2f-133">В следующем примере создается база данных с именем `mySampleDatabase`, в которую загружается образец данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="d8a2f-134">При необходимости замените эти предопределенные значения (другие краткие руководства в этой коллекции созданы на основе этого документа).</span><span class="sxs-lookup"><span data-stu-id="d8a2f-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="d8a2f-135">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="d8a2f-135">Clean up resources</span></span>

<span data-ttu-id="d8a2f-136">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="d8a2f-137">Если вы планируете продолжать работу с этими краткими руководствами, не удаляйте созданные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="d8a2f-138">Если вы не планируете продолжать работу, удалите все созданные ресурсы, выполнив на портале Azure следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="d8a2f-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8a2f-139">Next steps</span></span>

<span data-ttu-id="d8a2f-140">Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства.</span><span class="sxs-lookup"><span data-stu-id="d8a2f-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="d8a2f-141">См. дополнительные сведения о доступных средствах:</span><span class="sxs-lookup"><span data-stu-id="d8a2f-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="d8a2f-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d8a2f-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="d8a2f-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d8a2f-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="d8a2f-144">.NET</span><span class="sxs-lookup"><span data-stu-id="d8a2f-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="d8a2f-145">PHP</span><span class="sxs-lookup"><span data-stu-id="d8a2f-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="d8a2f-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="d8a2f-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="d8a2f-147">Java</span><span class="sxs-lookup"><span data-stu-id="d8a2f-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="d8a2f-148">Python</span><span class="sxs-lookup"><span data-stu-id="d8a2f-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="d8a2f-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="d8a2f-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

