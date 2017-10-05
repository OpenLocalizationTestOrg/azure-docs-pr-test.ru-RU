---
title: "Перенос базы данных с помощью импорта и экспорта в базе данных Azure для PostgreSQL | Документация Майкрософт"
description: "Описывается, как извлечь базу данных PostgreSQL в файл сценария и импортировать данные из этого файла в целевую базу данных."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="687c5-103">Перенос базы данных PostgreSQL с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="687c5-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="687c5-104">Можно извлечь базу данных PostgreSQL в файл сценария с помощью [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) и импортировать данные из этого файла в целевую базу данных с помощью [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="687c5-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="687c5-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="687c5-105">Prerequisites</span></span>
<span data-ttu-id="687c5-106">Прежде чем приступить к выполнению этого руководства, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="687c5-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="687c5-107">[сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-portal.md) с правилами брандмауэра, разрешающими доступ к этом серверу и его базам данных;</span><span class="sxs-lookup"><span data-stu-id="687c5-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="687c5-108">установленная программа командной строки [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html);</span><span class="sxs-lookup"><span data-stu-id="687c5-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="687c5-109">установленная программа командной строки [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="687c5-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="687c5-110">Выполните приведенные ниже действия, чтобы экспортировать и импортировать базу данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="687c5-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="687c5-111">Создание файла сценария, содержащего загружаемые данные, с помощью pg_dump</span><span class="sxs-lookup"><span data-stu-id="687c5-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="687c5-112">Чтобы экспортировать имеющуюся базу данных PostgreSQL в локальную среду или на виртуальную машину в виде файла сценария SQL, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="687c5-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="687c5-113">Например, если имеется локальный сервер с базой данных **testdb**.</span><span class="sxs-lookup"><span data-stu-id="687c5-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="687c5-114">Импорт данных в целевую базу данных Azure для PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="687c5-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="687c5-115">Можно использовать в командную строку psql с параметром -d, --dbname, чтобы импортировать данных в базу данных Azure для PostrgeSQL, которую мы создали, и загрузить данные из SQL-файла.</span><span class="sxs-lookup"><span data-stu-id="687c5-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="687c5-116">В этом примере используется программа psql и файл сценария **testdb.sql** из предыдущего шага, чтобы импортировать данные в базу данных **mypgsqldb** на целевом сервере **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="687c5-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="687c5-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="687c5-117">Next steps</span></span>
- <span data-ttu-id="687c5-118">Перенос базы данных PostgreSQL с помощью дампа и ее восстановление описывается в разделе [Перенос базы данных PostgreSQL с помощью дампа и ее восстановление](howto-migrate-using-dump-and-restore.md).</span><span class="sxs-lookup"><span data-stu-id="687c5-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>