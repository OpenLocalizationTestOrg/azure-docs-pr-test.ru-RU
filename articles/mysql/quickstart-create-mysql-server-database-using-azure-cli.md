---
title: "Краткое руководство. Создание базы данных Azure для сервера MySQL с помощью Azure CLI | Документация Майкрософт"
description: "В этом кратком руководстве описывается создание сервера базы данных Azure для MySQL в группе ресурсов Azure с помощью Azure CLI."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 11/29/2017
ms.custom: mvc
ms.openlocfilehash: aca5d33adda703f3cd50e940ee43bb0624e179a1
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Создание сервера базы данных Azure для MySQL с помощью Azure CLI
В этом кратком руководстве описывается создание сервера базы данных Azure для MySQL в группе ресурсов Azure с помощью Azure CLI за 5 минут. Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.

Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Если вы решили установить и использовать интерфейс командной строки локально, для работы с этой статьей вам понадобится Azure CLI 2.0 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Если вы используете несколько подписок, выберите соответствующую подписку, в которой находится ресурс либо в которой за него взимается плата. Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#az_account_set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов
Создайте [группу ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) с помощью команды [az group create](/cli/azure/group#az_group_create). Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.

В следующем примере создается группа ресурсов с именем `myresourcegroup` в расположении `westus`.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Создание сервера базы данных Azure для MySQL
Создайте сервер базы данных Azure для MySQL, выполнив команду **[az mysql server create](/cli/azure/mysql/server#az_mysql_server_create)**. Сервер может управлять несколькими базами данных. Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.

В следующем примере в группе ресурсов `myresourcegroup` создается сервер базы данных Azure для MySQL с именем `myserver4demo`, который расположен в `westus`. Для сервера указано имя администратора для входа `myadmin` и пароль `Password01!`. Он создается с уровнем производительности **Базовый** и **50** единицами вычислений, которые совместно используются всеми базами данных на сервере. В зависимости от потребностей приложения можно увеличить или уменьшить масштаб вычислительных ресурсов и ресурсов хранилища.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Настройка правила брандмауэра
Создайте правило брандмауэра на уровне сервера базы данных Azure для MySQL, выполнив команду **[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#az_mysql_server_firewall_rule_create)**. Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как программа командной строки **mysql.exe** или MySQL Workbench, подключаться к серверу через брандмауэр службы Azure MySQL. 

В примере ниже показано создание правила брандмауэра для предопределенного диапазона адресов, который в этом примере представляет наиболее полный диапазон IP-адресов.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Настройка параметров SSL
По умолчанию между сервером и клиентскими приложениями применяется SSL-соединение. Эта настройка по умолчанию гарантирует безопасное перемещение данных за счет шифрования потока данных через Интернет. Чтобы упростить работу с этим руководством, отключите SSL-соединения для вашего сервера. Мы не рекомендуем так делать для рабочих серверов. Дополнительные сведения см. в статье [Настройка SSL-подключений в приложении для безопасного подключения к базе данных Azure для MySQL](./howto-configure-ssl.md).

В следующем примере показано, как отключить SSL-соединение на сервере MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a>Получение сведений о подключении

Чтобы подключиться к серверу, необходимо указать сведения об узле и учетные данные для доступа.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Результаты выводятся в формате JSON. Запишите значения **fullyQualifiedDomainName** и **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a>Подключение к серверу с помощью программы командной строки mysql.exe
Подключитесь к серверу с помощью программы командной строки **mysql.exe**. MySQL можно скачать [здесь](https://dev.mysql.com/downloads/) и установить на компьютер. Вместо этого можно также нажать кнопку **Попробуйте!** в примерах кода или кнопку `>_` на панели инструментов в правом верхнем углу портала Azure и запустить **Azure Cloud Shell**.

Введите следующие команды. 

1. Подключитесь к серверу с помощью программы командной строки **mysql**:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Просмотрите состояние сервера:
```sql
 mysql> status
```
Если все работает правильно, в программе командной строки должен отобразиться следующий текст:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Дополнительные команды см. в [разделе 4.5.1 справочного руководства по MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a>Подключение к серверу с помощью инструмента графического пользовательского интерфейса MySQL Workbench
1.  Запустите приложение MySQL Workbench на клиентском компьютере. Скачать и установить MySQL Workbench вы можете [здесь](https://dev.mysql.com/downloads/workbench/).

2.  В диалоговом окне **настройки нового подключения** на вкладке **Параметры** введите следующие сведения:

   ![Настройка нового подключения](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Параметр** | **Рекомендуемое значение** | **Описание** |
|---|---|---|
|   Имя подключения | Мое подключение | Укажите любую метку для этого подключения. |
| Способ подключения | Выберите стандартный способ (по протоколу TCP/IP). | Используйте протокол TCP/IP для подключения к базе данных Azure для MySQL. |
| имя узла; | myserver4demo.mysql.database.azure.com | Имя сервера, которое вы записали ранее. |
| Порт | 3306 | Для MySQL используется порт по умолчанию. |
| Имя пользователя | myadmin@myserver4demo | Имя для входа администратора сервера, которое вы записали ранее. |
| Пароль | **** | Используйте пароль учетной записи администратора, настроенный ранее. |

Щелкните **Проверить подключение**, чтобы проверить, все ли параметры верно настроены.
Теперь можно щелкнуть только что созданное подключение, чтобы успешно подключиться к серверу.

## <a name="clean-up-resources"></a>Очистка ресурсов
Если эти ресурсы не требуются для изучения другого руководства, вы можете их удалить. Для этого выполните следующую команду: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Проектирование первой базы данных Azure для MySQL](./tutorial-design-database-using-cli.md)
