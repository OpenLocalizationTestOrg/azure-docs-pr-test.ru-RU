---
title: "aaaCreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью командной строки Azure CLI."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI
Правила брандмауэра уровня сервера включите tooan доступа toomanage администраторы базы данных Azure для сервера PostgreSQL определенный IP-адрес или диапазон IP-адресов. Командами удобный Azure CLI можно создать, обновить, удалить, а также выполнять их список и Показать toomanage правила брандмауэра сервера. Обзор брандмауэров базы данных Azure для PostgreSQL приведен в разделе [Правила брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);
- Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Настройка правил брандмауэра сервера базы данных Azure для PostgreSQL
Hello [az postgres правила брандмауэра для сервера —](/cli/azure/postgres/server/firewall-rule) команды, используемые tooconfigure правила брандмауэра.

## <a name="list-firewall-rules"></a>Вывод списка правил брандмауэра 
toolist hello существующих правил брандмауэра сервера на сервере hello запуска hello [список правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#list) команды.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
выходные данные Hello перечислены правила hello, если таковая имеется, по умолчанию в формате JSON формата. Можно использовать переключатель hello `--output table` для более удобочитаемый формат таблицы в качестве выходных данных hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Создание правила брандмауэра
новое правило брандмауэра на сервере hello, выполните hello toocreate [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) команды. 

В этом примере обеспечивает ряд все IP-адреса tooaccess hello сервера **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow единственном числе tooaccess IP адрес, укажите hello таким же адресом как hello начальный IP- и конечного IP-адресов, как показано в примере.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
После успешного выполнения выходные данные команды hello указаны подробности hello hello правило брандмауэра, которое вы создали, по умолчанию в формате JSON. В случае сбоя hello вместо вывода showserror текст сообщения.

## <a name="update-firewall-rule"></a>Обновление правила брандмауэра 
Обновление существующего правила брандмауэра на сервере с помощью hello [обновление правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#update) команды. Укажите имя hello существующее правило брандмауэра, как входные данные и hello начала IP-адресов и конечным IP атрибуты tooupdate hello.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
При успешном завершении hello выходные данные команды выводятся сведения hello hello правила брандмауэра, которые были обновлены, по умолчанию в формате JSON. В случае сбоя hello вместо вывода showserror текст сообщения.
> [!NOTE]
> Если правило брандмауэра hello не существует, он возвращает созданный командой обновления hello.

## <a name="show-firewall-rule-details"></a>Отображение сведений о правиле брандмауэра
Также можно показать существующий брандмауэра hello сведения о правиле, для сервера, запустив [Показать правила брандмауэра сервера postgres az](/cli/azure/postgres/server/firewall-rule#show) команды.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
После успешного выполнения выходные данные команды hello указаны подробности hello hello правило брандмауэра, которое вы задали, по умолчанию в формате JSON. В случае сбоя hello вместо вывода showserror текст сообщения.

## <a name="delete-firewall-rule"></a>Удаление правила брандмауэра
toorevoke доступ с сервера hello диапазона IP-удаление существующего правила брандмауэра, выполнив hello [az postgres правила брандмауэра для сервера — Удалить](/cli/azure/postgres/server/firewall-rule#delete) команды. Укажите имя hello hello существующее правило брандмауэра.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
При успешном выполнении выходные данные отсутствуют. При сбое возвращается сообщение об ошибке hello.

## <a name="next-steps"></a>Дальнейшие действия
- Аналогичным образом, можно использовать веб-браузер слишком[Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure](howto-manage-firewall-using-portal.md)
- Узнайте больше о [правилах брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md).
- Справку в подключении tooan базы данных Azure для сервера PostgreSQL см [библиотеки подключений к базе данных Azure для PostgreSQL](concepts-connection-libraries.md)
