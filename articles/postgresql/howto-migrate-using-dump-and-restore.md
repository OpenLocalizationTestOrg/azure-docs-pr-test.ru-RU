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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="844e5-103">Перенос базы данных PostgreSQL с помощью дампа и ее восстановление</span><span class="sxs-lookup"><span data-stu-id="844e5-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="844e5-104">Можно использовать [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL базы данных в файл дампа и [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore базы данных PostgreSQL hello из файла архива, созданного по pg_dump.</span><span class="sxs-lookup"><span data-stu-id="844e5-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="844e5-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="844e5-105">Prerequisites</span></span>
<span data-ttu-id="844e5-106">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="844e5-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="844e5-107">[Базы данных Azure для сервера PostgreSQL](quickstart-create-server-database-portal.md) с доступом tooallow правила брандмауэра и базы данных в нем.</span><span class="sxs-lookup"><span data-stu-id="844e5-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="844e5-108">установленные программы командной строки [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) и [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html).</span><span class="sxs-lookup"><span data-stu-id="844e5-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="844e5-109">Выполните эти шаги toodump и восстановление базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="844e5-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="844e5-110">Создание файла дампа с помощью pg_dump, содержащий toobe данных hello загружен</span><span class="sxs-lookup"><span data-stu-id="844e5-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="844e5-111">tooback копирование существующего PostgreSQL локальной базы данных или на виртуальной машине выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="844e5-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="844e5-112">Например, если имеется локальный сервер с базой данных **testdb**.</span><span class="sxs-lookup"><span data-stu-id="844e5-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="844e5-113">Для восстановления данных hello в hello целевой базы данных Azure для PostrgeSQL с помощью pg_restore</span><span class="sxs-lookup"><span data-stu-id="844e5-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="844e5-114">После создания hello целевой базы данных, можно использовать команду pg_restore hello и hello -d, параметр--dbname toorestore данных hello hello целевую базу данных из файла дампа hello.</span><span class="sxs-lookup"><span data-stu-id="844e5-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="844e5-115">В этом примере восстановить hello данные из файла дампа hello **testdb.dump** в базу данных hello **mypgsqldb** на целевом сервере **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="844e5-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="844e5-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="844e5-116">Next steps</span></span>
- <span data-ttu-id="844e5-117">. в разделе Использование функций экспорта и импорта базы данных PostgreSQL toomigrate [перенести базу данных PostgreSQL с помощью экспорта и импорта](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="844e5-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
