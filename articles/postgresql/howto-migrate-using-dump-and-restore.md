---
title: "aaaHow tooDump и восстановления в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Описывает, как tooextract PostgreSQL базы данных в файл дампа и восстановление базы данных PostgreSQL hello из созданных pg_dump в базе данных Azure для PostgreSQL архивного файла."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Перенос базы данных PostgreSQL с помощью дампа и ее восстановление
Можно использовать [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL базы данных в файл дампа и [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore базы данных PostgreSQL hello из файла архива, созданного по pg_dump.

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [Базы данных Azure для сервера PostgreSQL](quickstart-create-server-database-portal.md) с доступом tooallow правила брандмауэра и базы данных в нем.
- установленные программы командной строки [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) и [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html).

Выполните эти шаги toodump и восстановление базы данных PostgreSQL.

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Создание файла дампа с помощью pg_dump, содержащий toobe данных hello загружен
tooback копирование существующего PostgreSQL локальной базы данных или на виртуальной машине выполните hello следующую команду:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Например, если имеется локальный сервер с базой данных **testdb**.
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Для восстановления данных hello в hello целевой базы данных Azure для PostrgeSQL с помощью pg_restore
После создания hello целевой базы данных, можно использовать команду pg_restore hello и hello -d, параметр--dbname toorestore данных hello hello целевую базу данных из файла дампа hello.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
В этом примере восстановить hello данные из файла дампа hello **testdb.dump** в базу данных hello **mypgsqldb** на целевом сервере **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Дальнейшие действия
- . в разделе Использование функций экспорта и импорта базы данных PostgreSQL toomigrate [перенести базу данных PostgreSQL с помощью экспорта и импорта](howto-migrate-using-export-and-import.md)
