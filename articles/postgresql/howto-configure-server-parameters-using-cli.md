---
title: "Параметры службы aaaConfigure hello в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "В этой статье описывается, как параметры службы tooconfigure hello в базе данных Azure для использования PostgreSQL hello Azure CLI командной строки."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Настройка параметров конфигурации сервера с помощью Azure CLI
Можно перечислить, отображения и обновить параметры конфигурации для сервера Azure PostgreSQL, с помощью hello командной строки (CLI Azure). Однако только подмножество конфигураций ядра предоставляется на уровне сервера и может быть изменено. 

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);
- Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Получение списка параметров конфигурации сервера для базы данных Azure для сервера PostgreSQL
Запустите все изменяемые параметры сервера и соответствующие значения toolist hello [список конфигураций сервера postgres az](/cli/azure/postgres/server/configuration#list) команды.

Список параметров конфигурации сервера hello hello сервера можно **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Отображение сведений о параметре конфигурации сервера
tooshow сведения о параметре конкретной конфигурации для сервера, запустите hello [az postgres сервера конфигурации show](/cli/azure/postgres/server/configuration#show) команды.

В этом примере отображаются подробные сведения об hello **журнала\_min\_сообщений** параметр конфигурации сервера для сервера **mypgserver 20170401.postgres.database.azure.com** в группе Группа ресурсов **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Изменение значения параметра конфигурации сервера
Можно также изменить значение hello определенного параметра конфигурации сервера, и это обновляет hello базовое значение конфигурации для hello PostgreSQL server engine. конфигурации используйте tooupdate hello hello [набор конфигурации сервера postgres az](/cli/azure/postgres/server/configuration#set) команды. 

tooupdate hello **журнала\_min\_сообщений** параметр конфигурации сервера, сервера **mypgserver 20170401.postgres.database.azure.com** группересурсов**myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Если требуется tooreset hello значение параметра конфигурации, нужно просто выбрать tooleave out hello необязательно `--value` параметр и hello службы будет применяться значение по умолчанию hello. В приведенном выше примере это может выглядеть следующим образом.
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Это приведет к сбросу hello **журнала\_min\_сообщений** по умолчанию значения конфигурации toohello **предупреждение**. Дополнительные сведения о конфигурации сервера и допустимых значениях приведены в документации PostgreSQL по [конфигурации сервера](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Дальнейшие действия
- журналы сервера tooconfigure и доступа в разделе [журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md)
