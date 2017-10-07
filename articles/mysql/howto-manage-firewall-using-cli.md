---
title: "aaaCreate и управления базой данных Azure для MySQL правила брандмауэра, с помощью Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocreate и управления базой данных Azure для правил брандмауэра MySQL с помощью командной строки Azure CLI."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью Azure CLI
Правила брандмауэра уровня сервера включите tooan доступа toomanage администраторы базы данных Azure для сервера MySQL из определенный IP-адрес или диапазон IP-адресов. Командами удобный Azure CLI можно создать, обновить, удалить, а также выполнять их список и Показать toomanage правила брандмауэра сервера. Обзор брандмауэров базы данных Azure для MySQL приведен в разделе [Правила брандмауэра сервера базы данных Azure для MySQL](./concepts-firewall-rules.md).

## <a name="prerequisites"></a>Предварительные требования
* [Установите Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).
* Установите пакет SDK Azure для Python для служб MySQL и PostgreSQL.
* Установите компонент hello Azure CLI для служб, PostgreSQL и MySQL
* Создание сервера базы данных Azure для MySQL

## <a name="firewall-rule-commands"></a>Команды для правила брандмауэра
Hello **az mysql правила брандмауэра для сервера —** использовать команду из toocreate Azure CLI, удалить, список, отображения и обновить правила брандмауэра.

Команды:
- **create**: создание правила брандмауэра сервера Azure MySQL.
- **delete**: удаление правила брандмауэра сервера Azure MySQL.
- **список** : перечислить правила брандмауэра сервера Azure MySQL hello.
- **Показать** : Показать подробности hello сервера MySQL в Azure правило брандмауэра.
- **update**: обновление правила брандмауэра сервера Azure MySQL.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>TooAzure входа и список вашей базы данных Azure для серверов MySQL
Безопасно подключитесь к Azure CLI к помощью своей учетной записи Azure. Используйте hello **входа az** команды toodo это.

1. Выполните следующую команду из командной строки hello hello.
```azurecli
az login
```
Эта команда будет выдавать toouse кода hello следующем шаге.

2. На веб-страницу приветствия tooopen браузера [https://aka.ms/devicelogin](https://aka.ms/devicelogin) и введите код hello.

3. В строке приветствия вход, используя учетные данные Azure.

4. После авторизации имени входа в консоль hello будут выведены список подписок. Скопируйте идентификатор hello hello требуемого подписки tooset hello текущей подписки toobe используется продвижение вперед.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Список hello Azure баз данных MySQL серверов для вашей подписки и группе ресурсов, если вы не уверены приветствия имен.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Обратите внимание, атрибут имени hello в hello со списком, который будет использоваться toospecify какие toowork сервера MySQL на. При необходимости подтверждение hello сведения для этого toousing hello имя атрибута tooconfirm имя сервера указано правильно:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Вывод списка правил брандмауэра для сервера базы данных Azure для MySQL 
Используя hello имя сервера и имя группы ресурсов hello, список hello существующего правила брандмауэра для сервера на сервере hello. Обратите внимание, атрибут имени сервера hello указывается в hello **--сервер** переключения и не hello **--имя** переключения.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
Hello выходные данные будут отображаться hello правила, если таковая имеется, по умолчанию в формате JSON формата. Можно использовать переключатель hello **--выходная таблица** для более удобочитаемый формат таблицы в качестве выходных данных hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Создание правила брандмауэра для сервера базы данных Azure для MySQL
Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, создайте новое правило брандмауэра на сервере hello. Введите имя для правила hello, hello начальный IP-адрес и конечным IP для toocover hello правило доступа tooallow диапазон IP-адресов.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Для единственного IP адрес toobe доступ разрешен, предоставляют hello таким же адресом как hello начальный IP- и конечного IP-адресов, как показано в примере.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые вы создали, по умолчанию в формате JSON. В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Обновление правила брандмауэра для сервера базы данных Azure для MySQL 
С помощью hello Azure MySQL имя сервера и имя группы ресурсов hello, обновить существующее правило брандмауэра на сервере hello. Укажите имя hello существующее правило брандмауэра, как входные данные и hello начала IP-адресов и конечным IP атрибуты tooupdate hello.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые были обновлены, по умолчанию в формате JSON. В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.

> [!NOTE]
> Если правило брандмауэра hello не существует, создается командой обновления hello.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Отображение сведения о правиле брандмауэра для сервера базы данных Azure для MySQL
Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, подробно hello существующего брандмауэра правило с сервера hello. Предоставить имя hello hello существующее правило брандмауэра в качестве входных данных.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые указаны, по умолчанию в формате JSON. В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Удаление правила брандмауэра для сервера базы данных Azure для MySQL
Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, удалите существующее правило брандмауэра с сервера hello. Укажите имя hello hello существующее правило брандмауэра.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
При успешном выполнении выходные данные отсутствуют. После сбоя будет возвращено сообщение об ошибке hello.

## <a name="next-steps"></a>Дальнейшие действия
- Узнайте больше о [правилах брандмауэра сервера базы данных Azure для MySQL](./concepts-firewall-rules.md).
- [Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure](./howto-manage-firewall-using-portal.md)
