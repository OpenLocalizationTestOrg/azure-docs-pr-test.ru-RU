---
title: "Создание базы данных Azure для PostgreSQL, с помощью Azure CLI hello | Документы Microsoft"
description: "Быстрый запуск toocreate руководство по и управления базой данных Azure для сервера PostgreSQL, с помощью Azure CLI (интерфейс командной строки)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Создание базы данных Azure для PostgreSQL, с помощью hello Azure CLI
База данных Azure для PostgreSQL является управляемой службы, которая позволяет toorun, управлять и масштабировать высокодоступных баз данных PostgreSQL в облаке hello. Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. Краткого руководства показано, как toocreate Azure базы данных для сервера PostgreSQL в [группы ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) с помощью Azure CLI "hello".

Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

Если у вас несколько подписок, выберите нужную подписку hello, в котором будет выставлен счет hello ресурсов. Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа. Hello следующий пример создает группу ресурсов с именем `myresourcegroup` в hello `westus` расположение.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Создание сервера базы данных Azure для PostgreSQL

Создание [базы данных Azure для сервера PostgreSQL](overview.md) с помощью hello [az postgres server создать](/cli/azure/postgres/server#create) команды. Сервер содержит группу баз данных, которыми можно управлять как группой. 

Hello следующий пример создает сервер с именем `mypgserver-20170401` в группе ресурсов `myresourcegroup` с именем входа администратора сервера `mylogin`. Имя сервера Hello сопоставляет имя tooDNS и, таким образом необходимые toobe глобально уникальным в Azure. Замена hello `<server_admin_password>` с собственное значение.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> Имя входа администратора сервера Hello и пароль, указанные здесь являются необходимые toolog в toohello сервера и баз данных далее в этом кратком руководстве. Запомните или запишите эту информацию для последующего использования.

По умолчанию на сервере создается база данных **postgres**. Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) база данных является базой данных по умолчанию, предназначены для использования пользователями, служебные программы и сторонние приложения. 


## <a name="configure-a-server-level-firewall-rule"></a>Настройка правила брандмауэра на уровне сервера

Создайте правило брандмауэра уровня сервера Azure PostgreSQL с hello [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) команды. Правила брандмауэра уровня сервера позволяет внешнего приложения, такие как [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) или [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server через брандмауэр службы Azure PostgreSQL hello. 

Можно задать правило брандмауэра, которое охватывает IP диапазон toobe может tooconnect из сети. Hello следующий пример использует [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) toocreate правило брандмауэра `AllowAllIps` IP-адрес диапазона адресов. tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Сервер PostgreSQL Azure обменивается данными через порт 5432. При попытках подключения из корпоративной сети может оказаться, что исходящий трафик через порт 5432 запрещен сетевым брандмауэром. Есть открыть порт сервера базы данных SQL Azure на 5432 tooconnect tooyour ИТ-отдела.

## <a name="get-hello-connection-information"></a>Получить сведения о соединении hello

tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

Hello получается в формате JSON. Запишите hello **Имя_входа_администратора** и **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-toopostgresql-database-using-psql"></a>Подключитесь с помощью psql базу данных tooPostgreSQL

Если клиентский компьютер имеет PostgreSQL установлен, можно использовать локальный экземпляр [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL сервера. Теперь воспользуемся hello psql программы командной строки tooconnect toohello Azure PostgreSQL сервера.

1. Запустите следующие команды psql tooconnect tooan базы данных Azure для сервера PostgreSQL hello
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Например, следующую команду hello подключается toohello по умолчанию база данных с именем **postgres** на сервере PostgreSQL **mypgserver 20170401.postgres.database.azure.com** с использованием учетных данных. Введите hello `<server_admin_password>` вы выбрали при запросе пароля.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  После toohello подключенного сервера, создайте пустую базу данных в строке приветствия.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Выполните следующие tooswitch для команды подключение к базе данных только что созданный toohello hello строке hello **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Подключитесь с помощью pgAdmin базу данных tooPostgreSQL

с помощью средства hello графического интерфейса пользователя PostgreSQL сервера с tooAzure tooconnect _pgAdmin_
1.  Запустите hello _pgAdmin_ приложения на клиентском компьютере. Вы можете установить _pgAdmin_ с помощью http://www.pgadmin.org/.
2.  Выберите **добавить новый сервер** из hello **быстрые ссылки** меню.
3.  В hello **создание - сервера** диалоговое окно **Общие** введите уникальное понятное имя для сервера hello. Например, **Azure PostgreSQL Server**.
 ![Средство pgAdmin. Создание сервера](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  В hello **создание - сервера** диалоговом **подключения** вкладки:
    - Введите hello полное имя сервера (например, **mypgserver 20170401.postgres.database.azure.com**) в hello **имя узла / адрес** поле. 
    - Введите порт 5432 в hello **порт** поле. 
    - Введите hello **имя входа администратора сервера (user@mypgserver)** полученные ранее в данном краткое руководство и пароль, введенный при создании сервера hello в hello **Username** и **пароля** соответственно.
    - Выберите для **режима SSL** значение **Запросить**. По умолчанию все серверы PostgreSQL Azure создаются с включенным применением SSL. tooturn OFF применяют SSL, см. Подробности в [применения SSL](./concepts-ssl-connection-security.md).

    ![pgAdmin. Создание сервера](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Щелкните **Сохранить**.
6.  В левой области обозревателя hello разверните hello **групп серверов**. Выберите свой сервер **Azure PostgreSQL Server**.
7.  Выберите hello **сервера** подключены, а затем выберите **баз данных** под ним. 
8.  Щелкните правой кнопкой мыши **баз данных** tooCreate базы данных.
9.  Выберите имя базы данных **mypgsqldb** и hello владельца для него, что имя входа администратора сервера **пользователь**.
10. Нажмите кнопку **Сохранить** toocreate пустую базу данных.
11. В hello **браузера**, разверните hello **серверы** группы. Разверните сервер hello, вы создали и см. база данных hello **mypgsqldb** под ним.
 ![pgAdmin. Создание базы данных](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Очистка ресурсов

Очистить все ресурсы, созданные в кратком руководстве hello, удалив hello [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Другие краткие руководства в этой коллекции созданы на основе этого документа. Если вы планируете toowork с последующей toocontinue краткие руководства, выполните очистку не hello ресурсы, созданные в этом кратком руководстве. Если вы не планируете toocontinue, используйте следующие шаги toodelete hello все ресурсы, созданные в этом кратком руководстве в hello Azure CLI.

```azurecli-interactive
az group delete --name myresourcegroup
```

Если вы просто хотите toodelete hello один только что созданный сервер, можно запустить [удаления сервера postgres az](/cli/azure/postgres/server#delete) команды.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./howto-migrate-using-export-and-import.md)
