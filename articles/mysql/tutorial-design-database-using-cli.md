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
# <a name="design-your-first-azure-database-for-mysql-database"></a>Проектирование первой базы данных Azure для MySQL

База данных Azure для MySQL — это служба реляционной базы данных в зависимости от базы данных MySQL Community Edition Microsoft cloud hello. В этом учебнике используется Azure CLI (интерфейс командной строки) и другие служебные программы toolearn как для:

> [!div class="checklist"]
> * создание базы данных Azure для MySQL;
> * Настройте брандмауэр сервера hello
> * Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate базы данных
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
Создайте [группу ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview), выполнив команду [az group create](https://docs.microsoft.com/cli/azure/group#create). Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.

Hello следующий пример создает группу ресурсов с именем `mycliresource` в hello `westus` расположение.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Создание сервера базы данных Azure для MySQL
Можно создайте базу данных Azure для сервера MySQL с помощью сервера mysql az hello создать команду. Сервер может управлять несколькими базами данных. Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.

Hello следующий пример создает базы данных Azure для MySQL server, расположенный в `westus` в группе ресурсов hello `mycliresource` с именем `mycliserver`. Hello сервер имеет журнал администратора в с именем `myadmin` и пароль `Password01!`. сервер Hello создается с **основные** уровня производительности и **50** единиц, общим для всех баз данных hello в hello server вычислительных операций. Вычислений и хранилища можно масштабировать вверх или вниз в зависимости от потребностей приложения hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Настройка правила брандмауэра
Можно создайте базу данных Azure для правила брандмауэра уровня сервера MySQL с hello az mysql правила брандмауэра для сервера — команда «Создать». Правила брандмауэра уровня сервера позволяет внешнего приложения, такие как **mysql** средство командной строки или MySQL Workbench tooconnect tooyour server через брандмауэр службы MySQL в Azure hello. 

Hello следующий пример создает правило брандмауэра для предопределенный адрес диапазона. Этот пример hello все возможные диапазон IP-адресов.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Получить сведения о соединении hello

tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

Hello получается в формате JSON. Запишите hello **fullyQualifiedDomainName** и **Имя_входа_администратора**.
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

## <a name="connect-toohello-server-using-mysql"></a>Подключиться с помощью mysql server toohello
Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour подключения базы данных Azure для сервера MySQL. В этом примере команда hello имеет вид:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Создание пустой базы данных
Когда вы будете toohello подключенного сервера, создайте пустую базу данных.
```sql
mysql> CREATE DATABASE mysampledb;
```

В строке приветствия выполните hello, выполнив команду подключения hello tooswitch toothis вновь созданные базы данных:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Создание таблиц в базе данных hello
Теперь, когда вы знаете, как tooconnect toohello базы данных Azure для базы данных MySQL, мы можем открыть как toocomplete некоторых базовых задач.

Сначала можно создать таблицу и заполнить ее некоторыми данными. Давайте создадим таблицу, в которой хранятся данные инвентаризации.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Загрузка данных в таблицы hello
Теперь, когда таблица создана, мы можем вставить в нее данные. Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Теперь у вас две строки образца данных в таблицу hello, созданную ранее.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Запрашивать и обновлять данные hello в таблицах hello
Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello.
```sql
SELECT * FROM inventory;
```

Можно также обновить данные hello в таблицах hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Строка Hello обновляется соответствующим образом при извлечении данных.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Восстановление предыдущей точки tooa базы данных времени
Представьте, что вы случайно удалили таблицу. Восстановить ее будет не просто. Базы данных Azure для MySQL дает точки назад tooany toogo времени в hello последнего вверх too35 дни и в новом сервере tooa времени этой точки восстановления. Можно использовать этот новый сервер toorecover удаленные данные. Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.

Для восстановления hello требуется hello следующую информацию:

- Точка восстановления: выберите в момент, выполняемой до hello сервер был изменен. Должен быть больше или равен старые резервного копирования значение toohello базы данных-источника.
- Целевой сервер: Введите имя нового сервера требуется toorestore для
- Исходный сервер: укажите имя hello hello сервера, toorestore из
- Расположение: Не удается выбрать область hello, по умолчанию это то же, что hello исходного сервера

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

сервер toorestore hello и [восстановить tooa в момент](./howto-restore-server-portal.md) перед hello таблица была удалена. Восстановление сервера tooa другой момент времени, создает повторяющиеся новый сервер как исходный сервер hello как hello моменту времени можно указать, при условии, что он находится в пределах срока хранения hello вашей [уровня службы](./concepts-service-tiers.md).

## <a name="next-steps"></a>Дальнейшие действия
Из этого руководства вы узнали, как выполнять следующие операции:
> [!div class="checklist"]
> * создание базы данных Azure для MySQL;
> * Настройте брандмауэр сервера hello
> * Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate базы данных
> * Загрузка примера данных
> * Запрос данных
> * Обновление данных
> * восстановление данных.

> [!div class="nextstepaction"]
> [Примеры Azure CLI для базы данных Azure для MySQL](./sample-scripts-azure-cli.md)
