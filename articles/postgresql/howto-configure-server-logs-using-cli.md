---
title: "aaaConfigure и доступа в журналах сервера с помощью Azure CLI PostgreSQL | Документы Microsoft"
description: "В этой статье описывается, как tooconfigure и доступа hello в журналах сервера в базе данных Azure PostgreSQL, с помощью командной строки Azure CLI."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Настройка журналов сервера и получение к ним доступа с помощью Azure CLI
Можно загрузить с помощью командной строки (CLI Azure) hello ошибки журналы hello PostgreSQL сервера. Тем не менее журналы tootransaction доступа не поддерживается. 

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);
- Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Настройка ведения журнала для базы данных Azure для PostgreSQL
Можно настроить hello server tooaccess запроса журналы и журналы ошибок. Журналы ошибок могут содержать сведения об автоматической очистке, подключениях и контрольных точках.
1. Включите ведение журнала.
2. Журнал обновления\_инструкции и журнала\_min\_длительность\_ведение журнала запросов tooenable инструкции
3. Измените срок хранения.

Дополнительные сведения см. в статье [Настройка параметров конфигурации сервера с помощью Azure CLI](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Получение списка журналов для базы данных Azure для сервера PostgreSQL
toolist hello доступные файлы журнала для сервера, запустите hello [az postgres журналы сервера список](/cli/azure/postgres/server-logs#list) команды.

Можно получить список файлов журнала hello для сервера **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup**и направить его tooa текстовый файл с именем **журнала\_файлы\_list.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Локально загружать журналы с сервера hello
Hello [загрузить журналы сервера в postgres az](/cli/azure/postgres/server-logs#download) позволяет вам toodownload отдельные файлы журналов для вашего сервера. 

В этом примере загрузки hello файла журнала конкретного сервера hello **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup** tooyour локальной среде.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Дальнейшие действия
- toolearn Дополнительные сведения о журналах сервера. в разделе [журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md)
- Дополнительные сведения о параметрах сервера см. в статье [Настройка параметров конфигурации сервера с помощью Azure CLI](howto-configure-server-parameters-using-cli.md).
