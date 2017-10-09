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
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Создание одной базы данных Azure SQL с помощью hello Azure CLI

Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. Это руководство сведений о toodeploy hello Azure CLI с помощью базы данных Azure SQL в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в [логический сервер базы данных SQL Azure](sql-database-features.md).

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Определение переменных

Определите переменные для использования в сценариях hello в этом кратком руководстве.

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

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Создание логического сервера

Создание [логический сервер базы данных SQL Azure](sql-database-features.md) с помощью hello [az sql server создавать](/cli/azure/sql/server#create) команды. Логический сервер содержит группу баз данных, которыми можно управлять как группой. Hello следующий пример создает произвольным именем сервера в группе ресурсов с именем входа администратора с именем `ServerAdmin` и паролем `ChangeYourAdminPassword1`. Замените эти предопределенные значения по своему усмотрению.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Настройка правил брандмауэра сервера

Создание [правила брандмауэра уровня сервера базы данных SQL Azure](sql-database-firewall-configure.md) с помощью hello [создать брандмауэр сервера sql az](/cli/azure/sql/server/firewall-rule#create) команды. Правила брандмауэра уровня сервера позволяет внешнему приложению, например SQL Server Management Studio или hello SQLCMD программа tooconnect tooa SQL базы данных через брандмауэр службы hello базы данных SQL. В следующем примере hello брандмауэр hello открыт только для других ресурсов Azure. tooenable возможности внешнего подключения, изменение hello tooan соответствующий адрес для вашей среды. tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> База данных SQL обменивается данными через порт 1433. Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети. В этом случае нельзя сервера базы данных SQL Azure может tooconnect tooyour Если ИТ-отдел открывает порт 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Создайте базу данных сервера hello с образцами данных

Создание базы данных с [уровень производительности не ниже S0](sql-database-service-tiers.md) в hello server с помощью hello [создание баз данных SQL Server az](/cli/azure/sql/db#create) команды. Hello следующий пример создает базу данных с именем `mySampleDatabase` и загружает hello AdventureWorksLT образец данных в эту базу данных. В случае необходимости заменить эти предопределенные значения (другие краткие в этой сборке коллекции на hello значения в этом кратком руководстве).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Другие краткие руководства в этой коллекции созданы на основе этого документа. 

> [!TIP]
> Если планируется toocontinue toowork с последующей краткие, не очистки hello ресурсы, созданные в этом быстрого запускаются. Если вы не планируете toocontinue, используйте следующие шаги toodelete все ресурсы, которые созданы в этом кратком руководстве в hello портал Azure hello.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства. См. дополнительные сведения о доступных средствах:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

