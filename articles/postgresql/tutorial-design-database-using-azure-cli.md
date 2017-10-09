---
title: "Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI | Документация Майкрософт"
description: "В этом учебнике показано, как tooDesign Azure первой базы данных для PostgreSQL с помощью Azure CLI."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI 
В этом учебнике используется Azure CLI (интерфейс командной строки) и другие служебные программы toolearn как для:
> [!div class="checklist"]
> * Создание базы данных Azure для PostgreSQL
> * Настройте брандмауэр сервера hello
> * Используйте [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate программа базы данных
> * Загрузка примера данных
> * Запрос данных
> * Обновление данных
> * восстановление данных.

Вы можете использовать hello оболочки облако Azure в обозревателе hello, или [установить CLI Azure 2.0]( /cli/azure/install-azure-cli) на блоки собственного компьютера toorun hello в этом учебнике.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

Если у вас несколько подписок, выберите нужную подписку hello, в котором hello ресурсов существует, или плата за. Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).
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

Hello следующий пример создает сервер называется `mypgserver-20170401` в группе ресурсов `myresourcegroup` с именем входа администратора сервера `mylogin`. Имя учетной записи для сопоставления имени tooDNS и, таким образом необходимые toobe глобально уникальным в Azure. Замена hello `<server_admin_password>` с собственное значение.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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
>

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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Подключение tooAzure базы данных для базы данных PostgreSQL, с помощью psql
Если клиентский компьютер имеет PostgreSQL установлен, можно использовать локальный экземпляр [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), или hello Azure облачной tooconnect tooan Azure PostgreSQL сервера консоли. Теперь воспользуемся hello psql программы командной строки tooconnect toohello базы данных Azure для сервера PostgreSQL.

1. Запустите следующие команды psql tooconnect tooan базы данных Azure для сервера PostgreSQL hello
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Например, следующую команду hello подключается toohello по умолчанию база данных с именем **postgres** на сервере PostgreSQL **mypgserver 20170401.postgres.database.azure.com** с использованием учетных данных. Введите hello `<server_admin_password>` вы выбрали при запросе пароля.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  После toohello подключенного сервера, создайте пустую базу данных в строке приветствия.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Выполните следующие tooswitch для команды подключение к базе данных только что созданный toohello hello строке hello **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Создание таблиц в базе данных hello
Теперь, когда вы знаете, как toohello tooconnect базы данных Azure для PostgreSQL, мы можем открыть как toocomplete некоторых базовых задач.

Сначала можно создать таблицу и заполнить ее некоторыми данными. Давайте создадим таблицу, с помощью которой можно отслеживать данные инвентаризации.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Вы можете увидеть hello вновь созданные таблицы в списке hello таблиц теперь, введя:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Загрузка данных в таблицы hello
Теперь, когда таблица создана, мы можем вставить в нее данные. Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

У вас теперь две строки образца данных в таблицу hello, созданную ранее.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Запрашивать и обновлять данные hello в таблицах hello
Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello. 
```sql
SELECT * FROM inventory;
```

Можно также обновить данные hello в таблицах hello
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Строка Hello обновляется соответствующим образом при извлечении данных.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Восстановление предыдущей точки tooa базы данных времени
Представьте, что вы случайно удалили таблицу. Восстановить ее будет не просто. База данных Azure для PostgreSQL позволяет toogo tooany назад в определенный момент (в hello последней копии too7 дней (Basic) и на 35 дней (стандартный)) и восстановления на момент tooa созданный сервер. Можно использовать этот новый сервер toorecover удаленные данные. Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` команда должна hello следующие параметры:
| Настройка | Рекомендуемое значение | Описание  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  Группа ресурсов, в которых hello исходный сервер существует.  |
| --name | mypgserver-restored | Имя Hello hello новый сервер, созданный команды restore hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Выберите на момент toorestore для. Дата и время должны находиться в пределах срока хранения резервной копии hello исходного сервера. Используйте формат даты и времени ISO8601. Например, вы можете использовать свой местный часовой пояс, например `2017-04-13T05:59:00-08:00`, или использовать формат UTC Zulu `2017-04-13T13:59:00Z`. |
| --source-server | mypgserver-20170401 | Hello имя или идентификатор hello исходного сервера toorestore из. |

Восстановление сервера tooa в момент создает новый сервер, копирование как hello исходного сервера hello на момент времени, указываемые. расположение Hello и ценах уровня значения для сервера восстановления hello hello аналогично hello исходного сервера.

Hello команда выполняется в синхронном режиме и вернет после восстановления сервера hello. После завершения выполнения hello восстановления, найдите hello новый сервер, который был создан. Проверьте приветствия восстановления данных должным образом.


## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, каким образом toouse Azure CLI (интерфейс командной строки) и других служебных программ для:
> [!div class="checklist"]
> * Создание базы данных Azure для PostgreSQL
> * Настройте брандмауэр сервера hello
> * Используйте [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate программа базы данных
> * Загрузка примера данных
> * Запрос данных
> * Обновление данных
> * восстановление данных.

Далее, узнайте, как toouse hello Azure портала toodo других подобных задач, просмотрите этот учебник: [конструкцию первой базы данных Azure с помощью PostgreSQL hello портал Azure](tutorial-design-database-using-azure-portal.md)
