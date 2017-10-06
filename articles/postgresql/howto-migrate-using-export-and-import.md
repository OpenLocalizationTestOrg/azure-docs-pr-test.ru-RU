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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="259a7-103">Перенос базы данных PostgreSQL с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="259a7-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="259a7-104">Можно использовать [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL базы данных в файл скрипта и [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport данных hello в hello целевую базу данных из этого файла.</span><span class="sxs-lookup"><span data-stu-id="259a7-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="259a7-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="259a7-105">Prerequisites</span></span>
<span data-ttu-id="259a7-106">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="259a7-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="259a7-107">[Базы данных Azure для сервера PostgreSQL](quickstart-create-server-database-portal.md) с доступом tooallow правила брандмауэра и базы данных в нем.</span><span class="sxs-lookup"><span data-stu-id="259a7-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="259a7-108">установленная программа командной строки [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html);</span><span class="sxs-lookup"><span data-stu-id="259a7-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="259a7-109">установленная программа командной строки [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="259a7-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="259a7-110">Выполните эти шаги tooexport и импорта базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="259a7-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="259a7-111">Создание файла скрипта с помощью pg_dump, содержащий toobe данных hello загружен</span><span class="sxs-lookup"><span data-stu-id="259a7-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="259a7-112">tooexport вашей существующей PostgreSQL локальной базы данных или в файл скрипта sql tooa виртуальной Машины выполните следующую команду в существующей среде hello:</span><span class="sxs-lookup"><span data-stu-id="259a7-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="259a7-113">Например, если имеется локальный сервер с базой данных **testdb**.</span><span class="sxs-lookup"><span data-stu-id="259a7-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="259a7-114">Импорт данных hello в целевой базе данных Azure для PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="259a7-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="259a7-115">Можно использовать hello psql командной строки и hello -d,--dbname параметр tooimport hello данных в базе данных Azure для PostrgeSQL мы создания и загрузки данных из файла sql hello.</span><span class="sxs-lookup"><span data-stu-id="259a7-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="259a7-116">В этом примере используется программа psql и файл скрипта с именем **testdb.sql** из предыдущих данных tooimport шаг в базу данных hello **mypgsqldb** на целевом сервере  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="259a7-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="259a7-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="259a7-117">Next steps</span></span>
- <span data-ttu-id="259a7-118">toomigrate базы данных PostgreSQL, с помощью дампа и восстановление, в разделе [миграции с помощью дампа и восстановления базы данных PostgreSQL](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="259a7-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
