---
title: "Краткое руководство. Создание базы данных Azure для сервера MySQL с помощью Azure CLI | Документация Майкрософт"
description: "Это краткое руководство описывает, как toouse hello Azure CLI toocreate базы данных Azure для сервера MySQL в группе ресурсов Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Создание сервера базы данных Azure для MySQL с помощью Azure CLI
Это краткое руководство описывает, как toouse hello Azure CLI toocreate базы данных Azure для сервера MySQL в группе ресурсов Azure в около пяти минут. Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.

Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

Если у вас несколько подписок, выберите нужную подписку hello, в котором hello ресурсов существует, или плата за. Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов
Создание [группы ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) с помощью hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды. Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.

Hello следующий пример создает группу ресурсов с именем `myresourcegroup` в hello `westus` расположение.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Создание сервера базы данных Azure для MySQL
Создание базы данных Azure для сервера MySQL с hello **создать сервер mysql az** команды. Сервер может управлять несколькими базами данных. Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.

Hello следующий пример создает базы данных Azure для MySQL server, расположенный в `westus` в группе ресурсов hello `myresourcegroup` с именем `myserver4demo`. Hello сервер имеет журнал администратора в с именем `myadmin` и пароль `Password01!`. сервер Hello создается с **основные** уровня производительности и **50** единиц, общим для всех баз данных hello в hello server вычислительных операций. Вычислений и хранилища можно масштабировать вверх или вниз в зависимости от потребностей приложения hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Настройка правила брандмауэра
Создание базы данных Azure для правила брандмауэра уровня сервера MySQL с помощью hello **az mysql правила брандмауэра для сервера — создание** команды. Правила брандмауэра уровня сервера позволяет внешнему приложению, например hello **mysql.exe** средство командной строки или MySQL Workbench tooconnect tooyour server через брандмауэр службы MySQL в Azure hello. 

Hello следующий пример создает правило брандмауэра для диапазона предопределенный адрес, который в данном примере — hello все возможные диапазон IP-адресов.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Настройка параметров SSL
По умолчанию между сервером и клиентскими приложениями применяется SSL-соединение.  Это гарантирует безопасность «в движения» Здравствуйте, данных с помощью шифрования hello потока данных через Интернет.  toomake этого быстрого запуска проще, мы отключаем соединений SSL для сервера.  Мы не рекомендуем так делать для рабочих серверов.  Дополнительные сведения см. в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](./howto-configure-ssl.md).

Hello следующий пример отключает применение SSL для сервера MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Получить сведения о соединении hello

tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Hello получается в формате JSON. Запишите hello **fullyQualifiedDomainName** и **Имя_входа_администратора**.
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Подключение сервера toohello, с помощью средства командной строки mysql.exe hello
Подключение с помощью hello сервера tooyour **mysql.exe** средство командной строки. MySQL можно скачать [здесь](https://dev.mysql.com/downloads/) и установить на компьютер. Вместо этого можно также щелкнуть hello **попробовать** на образцы кода или hello `>_` кнопку hello верхней правой панели инструментов в hello портал Azure и запуска hello **оболочки облако Azure**.

Введите hello следующей команды: 

1. Подключение с использованием сервера toohello **mysql** средство командной строки:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Просмотрите состояние сервера:
```sql
 mysql> status
```
Если все пойдет хорошо, средство командной строки hello должен выводить hello следующий текст:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Подключение сервера toohello, с помощью средства графического интерфейса пользователя MySQL Workbench hello
1.  Запустите hello MySQL Workbench приложения на клиентском компьютере. Скачать и установить MySQL Workbench вы можете [здесь](https://dev.mysql.com/downloads/workbench/).

2.  В hello **установки нового подключения** диалогового окна введите следующую информацию hello **параметры** вкладки:

   ![Настройка нового подключения](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Параметр** | **Рекомендуемое значение** | **Описание** |
|---|---|---|
|   Имя подключения | Мое подключение | Укажите любую метку для этого подключения. |
| Способ подключения | Выберите стандартный способ (по протоколу TCP/IP). | Используйте для MySQL tooAzure tooconnect протокола TCP/IP базы данных > |
| имя узла; | myserver4demo.mysql.database.azure.com | Имя сервера, которое вы записали ранее. |
| Порт | 3306 | используется порт по умолчанию Hello для MySQL. |
| Имя пользователя | myadmin@myserver4demo | Hello сервера имя входа администратора, указанных выше. |
| Пароль | **** | Используйте пароль учетной записи администратора hello, настроенных ранее. |

Нажмите кнопку **проверить подключение** tootest, если все параметры настроены правильно.
Теперь можно щелкнуть подключение hello toosuccessfully подключения toohello сервера.

## <a name="clean-up-resources"></a>Очистка ресурсов
Если эти ресурсы не требуется для другой учебник, их можно удалить, выполнив следующую команду hello: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Проектирование первой базы данных Azure для MySQL](./tutorial-design-database-using-cli.md)
