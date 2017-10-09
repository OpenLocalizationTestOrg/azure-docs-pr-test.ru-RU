---
title: "Azure CLI: создание базы данных SQL | Документация Майкрософт"
description: "Узнайте, как toocreate логический сервер базы данных SQL, правила брандмауэра уровня сервера и баз данных с помощью hello Azure CLI."
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
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="e78df-104">Создание одной базы данных Azure SQL с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e78df-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="e78df-105">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="e78df-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="e78df-106">Это руководство сведений о toodeploy hello Azure CLI с помощью базы данных Azure SQL в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в [логический сервер базы данных SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="e78df-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="e78df-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e78df-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e78df-108">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e78df-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e78df-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e78df-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e78df-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e78df-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="e78df-111">Определение переменных</span><span class="sxs-lookup"><span data-stu-id="e78df-111">Define variables</span></span>

<span data-ttu-id="e78df-112">Определите переменные для использования в сценариях hello в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="e78df-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="e78df-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e78df-113">Create a resource group</span></span>

<span data-ttu-id="e78df-114">Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e78df-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e78df-115">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="e78df-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="e78df-116">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение.</span><span class="sxs-lookup"><span data-stu-id="e78df-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="e78df-117">Создание логического сервера</span><span class="sxs-lookup"><span data-stu-id="e78df-117">Create a logical server</span></span>

<span data-ttu-id="e78df-118">Создание [логический сервер базы данных SQL Azure](sql-database-features.md) с помощью hello [az sql server создавать](/cli/azure/sql/server#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e78df-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="e78df-119">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="e78df-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="e78df-120">Hello следующий пример создает произвольным именем сервера в группе ресурсов с именем входа администратора с именем `ServerAdmin` и паролем `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="e78df-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="e78df-121">Замените эти предопределенные значения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="e78df-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="e78df-122">Настройка правил брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="e78df-122">Configure a server firewall rule</span></span>

<span data-ttu-id="e78df-123">Создание [правила брандмауэра уровня сервера базы данных SQL Azure](sql-database-firewall-configure.md) с помощью hello [создать брандмауэр сервера sql az](/cli/azure/sql/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e78df-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="e78df-124">Правила брандмауэра уровня сервера позволяет внешнему приложению, например SQL Server Management Studio или hello SQLCMD программа tooconnect tooa SQL базы данных через брандмауэр службы hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e78df-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="e78df-125">В следующем примере hello брандмауэр hello открыт только для других ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e78df-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="e78df-126">tooenable возможности внешнего подключения, изменение hello tooan соответствующий адрес для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e78df-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="e78df-127">tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="e78df-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="e78df-128">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="e78df-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="e78df-129">Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети.</span><span class="sxs-lookup"><span data-stu-id="e78df-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="e78df-130">В этом случае нельзя сервера базы данных SQL Azure может tooconnect tooyour Если ИТ-отдел открывает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="e78df-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="e78df-131">Создайте базу данных сервера hello с образцами данных</span><span class="sxs-lookup"><span data-stu-id="e78df-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="e78df-132">Создание базы данных с [уровень производительности не ниже S0](sql-database-service-tiers.md) в hello server с помощью hello [создание баз данных SQL Server az](/cli/azure/sql/db#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e78df-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="e78df-133">Hello следующий пример создает базу данных с именем `mySampleDatabase` и загружает hello AdventureWorksLT образец данных в эту базу данных.</span><span class="sxs-lookup"><span data-stu-id="e78df-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="e78df-134">В случае необходимости заменить эти предопределенные значения (другие краткие в этой сборке коллекции на hello значения в этом кратком руководстве).</span><span class="sxs-lookup"><span data-stu-id="e78df-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="e78df-135">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e78df-135">Clean up resources</span></span>

<span data-ttu-id="e78df-136">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="e78df-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="e78df-137">Если планируется toocontinue toowork с последующей краткие, не очистки hello ресурсы, созданные в этом быстрого запускаются.</span><span class="sxs-lookup"><span data-stu-id="e78df-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="e78df-138">Если вы не планируете toocontinue, используйте следующие шаги toodelete все ресурсы, которые созданы в этом кратком руководстве в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e78df-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="e78df-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e78df-139">Next steps</span></span>

<span data-ttu-id="e78df-140">Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства.</span><span class="sxs-lookup"><span data-stu-id="e78df-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="e78df-141">См. дополнительные сведения о доступных средствах:</span><span class="sxs-lookup"><span data-stu-id="e78df-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="e78df-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="e78df-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="e78df-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e78df-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="e78df-144">.NET</span><span class="sxs-lookup"><span data-stu-id="e78df-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="e78df-145">PHP</span><span class="sxs-lookup"><span data-stu-id="e78df-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="e78df-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="e78df-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="e78df-147">Java</span><span class="sxs-lookup"><span data-stu-id="e78df-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="e78df-148">Python</span><span class="sxs-lookup"><span data-stu-id="e78df-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="e78df-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="e78df-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

