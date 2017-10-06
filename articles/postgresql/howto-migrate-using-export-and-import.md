---
title: "aaaMigrate базы данных путем импорта и экспорта в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Описывает способ извлечения данных PostgreSQL в файл скрипта и импортировать данные hello в hello целевую базу данных из этого файла."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Перенос базы данных PostgreSQL с помощью экспорта и импорта
Можно использовать [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL базы данных в файл скрипта и [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport данных hello в hello целевую базу данных из этого файла.

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [Базы данных Azure для сервера PostgreSQL](quickstart-create-server-database-portal.md) с доступом tooallow правила брандмауэра и базы данных в нем.
- установленная программа командной строки [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html);
- установленная программа командной строки [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html).

Выполните эти шаги tooexport и импорта базы данных PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Создание файла скрипта с помощью pg_dump, содержащий toobe данных hello загружен
tooexport вашей существующей PostgreSQL локальной базы данных или в файл скрипта sql tooa виртуальной Машины выполните следующую команду в существующей среде hello:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Например, если имеется локальный сервер с базой данных **testdb**.
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Импорт данных hello в целевой базе данных Azure для PostrgeSQL
Можно использовать hello psql командной строки и hello -d,--dbname параметр tooimport hello данных в базе данных Azure для PostrgeSQL мы создания и загрузки данных из файла sql hello.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
В этом примере используется программа psql и файл скрипта с именем **testdb.sql** из предыдущих данных tooimport шаг в базу данных hello **mypgsqldb** на целевом сервере  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Дальнейшие действия
- toomigrate базы данных PostgreSQL, с помощью дампа и восстановление, в разделе [миграции с помощью дампа и восстановления базы данных PostgreSQL](howto-migrate-using-dump-and-restore.md)
