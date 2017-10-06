---
title: "Как tooback копировании и восстановлении сервера базы данных Azure для PostgreSQL | Документы Microsoft"
description: "Узнайте, как tooback копирование и восстановление сервера в базе данных Azure для PostgreSQL с помощью hello Azure CLI."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Здравствуйте как tooback копирование и восстановление сервера в базе данных Azure для PostgreSQL с помощью Azure CLI

Использование базы данных Azure для PostgreSQL toorestore tooan сервера базы данных более ранней даты, охватывающий 7 дней too35.

## <a name="prerequisites"></a>Предварительные требования
toocomplete как tooguide, необходимо:
- [сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Если установить и использовать hello Azure CLI локально, это как tooguide требует использования Azure CLI версии 2.0 или более поздней версии. версия tooconfirm hello, hello Azure CLI командной строки, введите `az --version`. tooinstall или обновления, см. в [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>Резервное копирование выполняется автоматически
При использовании базы данных Azure для PostgreSQL hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут. 

Для базового уровня hello резервные копии доступны в течение 7 дней. Для уровня Standard hello доступны архивы 35 дней. Дополнительные сведения см. в статье [Параметры и производительность базы данных Azure для PostgreSQL: возможности, доступные в каждой ценовой категории](concepts-service-tiers.md).

Благодаря этому автоматического резервного копирования восстановления сервера hello и его tooan баз данных более ранней датой или на определенный момент времени.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Восстановление базы данных предыдущей точки tooa времени с помощью hello Azure CLI
Использование базы данных Azure для PostgreSQL toorestore hello server tooa предыдущий момент времени. Hello восстановить данные копируются tooa новый сервер, и существующий сервер hello оставляется. Например если таблица случайно удалена в полдень сегодня, можно восстановить время toohello только до полудня. Затем можно получить hello отсутствует таблицы и данные из копии восстановить hello hello server. 

toorestore hello server, используйте hello Azure CLI [восстановление server postgres az](/cli/azure/postgres/server#restore) команды.

### <a name="run-hello-restore-command"></a>Выполните команду restore hello

сервер hello toorestore, hello Azure CLI командной строки, введите следующую команду hello:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` команды необходим hello следующие параметры:
| Настройка | Рекомендуемое значение | Описание  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  Группа ресурсов, где существует hello исходного сервера.  |
| name | mypgserver-restored | Имя Hello hello новый сервер, созданный команды restore hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Выберите конкретное время toorestore для. Дата и время должны находиться в hello исходного сервера резервное копирование срока хранения. Использование формата hello ISO8601 даты и времени. Можно использовать местный часовой пояс, например `2017-04-13T05:59:00-08:00`. Можно также использовать hello, формат UTC Zulu, например, `2017-04-13T13:59:00Z`. |
| source-server | mypgserver-20170401 | Hello имя или идентификатор hello исходного сервера toorestore из. |

При восстановлении tooan сервера более раннего момента времени, создается новый сервер. Hello исходного сервера и баз данных из hello указанные точки во времени, скопированный toohello новый сервер.

значения уровня место и ценах Hello для сервера восстановления hello оставаться hello таким же как hello исходного сервера. 

Hello `az postgres server restore` команда является синхронным. После восстановления сервера hello вы можно использовать снова toorepeat hello процесс для другой момент времени. 

После hello завершения процесса восстановления, найдите новый сервер hello и убедитесь, что hello данные восстанавливаются должным образом.

## <a name="next-steps"></a>Дальнейшие действия
[Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md)
