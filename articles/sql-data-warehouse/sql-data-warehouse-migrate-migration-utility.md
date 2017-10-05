---
title: "Перенос: служебная программа для переноса в хранилище данных | Документация Майкрософт"
description: "Миграция в хранилище данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 2466e823c448ada4dc7bc5769b1b7f10bbb5dc7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="c1314-103">Служебная программа для миграции в хранилище данных (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c1314-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c1314-104">[Скачивание служебной программы переноса][Download Migration Utility]</span><span class="sxs-lookup"><span data-stu-id="c1314-104">[Download Migration Utility][Download Migration Utility]</span></span>
> 
> 

<span data-ttu-id="c1314-105">Служебная программа для миграции в хранилище данных — это средство, предназначенное для переноса схемы и данных с сервера SQL Server и из базы данных SQL Azure в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c1314-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c1314-106">Во время переноса схемы средство автоматически сопоставляет соответствующую схему из источника с местом назначения.</span><span class="sxs-lookup"><span data-stu-id="c1314-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span></span> <span data-ttu-id="c1314-107">После переноса схемы средство предоставляет возможность переместить данные с помощью автоматически создаваемых сценариев.</span><span class="sxs-lookup"><span data-stu-id="c1314-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span></span>

<span data-ttu-id="c1314-108">С помощью этого средства можно не только переносить схемы и данные, но и создавать отчеты о совместимости. В этих отчетах содержится сводка проблем совместимости между целевым и исходным экземплярами, препятствующих оптимизированной миграции.</span><span class="sxs-lookup"><span data-stu-id="c1314-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="c1314-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c1314-109">Get started</span></span>
<span data-ttu-id="c1314-110">Перед началом установки потребуется служебная программа командной строки BCP для запуска сценариев миграции и система Office для просмотра отчета о совместимости.</span><span class="sxs-lookup"><span data-stu-id="c1314-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span></span> <span data-ttu-id="c1314-111">После запуска загруженного исполняемого файла вам будет предложено принять условия стандартного лицензионного соглашения, прежде чем начнется установка.</span><span class="sxs-lookup"><span data-stu-id="c1314-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span></span>

<span data-ttu-id="c1314-112">Кроме того, для запуска служебной программы миграции требуется одно из следующих разрешений для базы данных, которую необходимо перенести: CREATE DATABASE, ALTER ANY DATABASE или VIEW ANY DEFINITION.</span><span class="sxs-lookup"><span data-stu-id="c1314-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-the-tool-and-connecting"></a><span data-ttu-id="c1314-113">Запуск инструмента и подключение</span><span class="sxs-lookup"><span data-stu-id="c1314-113">Launching the tool and connecting</span></span>
<span data-ttu-id="c1314-114">Запустите инструмент, щелкнув значок на рабочем столе, который появляется после установки.</span><span class="sxs-lookup"><span data-stu-id="c1314-114">Launch the tool by clicking on the desktop icon which appears post install.</span></span> <span data-ttu-id="c1314-115">При открытии средства отобразится начальная страница подключения, где можно выбрать источник и место назначения для миграции.</span><span class="sxs-lookup"><span data-stu-id="c1314-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span></span> <span data-ttu-id="c1314-116">В настоящее время в качестве источников поддерживаются сервер SQL Server и База данных SQL Azure, а в качестве места назначения — хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c1314-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="c1314-117">После выбора этих параметров появится запрос на подключение к исходному серверу. Для этого нужно ввести имя сервера, пройти проверку подлинности и нажать кнопку «Подключить».</span><span class="sxs-lookup"><span data-stu-id="c1314-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="c1314-118">После проверки подлинности откроется список баз данных на подключенном сервере.</span><span class="sxs-lookup"><span data-stu-id="c1314-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span></span> <span data-ttu-id="c1314-119">Чтобы начать миграцию, выберите базу данных, которую следует перенести, и нажмите кнопку "Перенести выбранные".</span><span class="sxs-lookup"><span data-stu-id="c1314-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="c1314-120">Отчет о миграции</span><span class="sxs-lookup"><span data-stu-id="c1314-120">Migration report</span></span>
<span data-ttu-id="c1314-121">Если выбрать в средстве миграции команду "Проверить совместимость базы данных", будет создан сводный отчет по всем проблемам совместимости в объектах базы данных, которую требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="c1314-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span></span> <span data-ttu-id="c1314-122">Расширенный список функций сервера SQL Server, отсутствующих в хранилище данных SQL, см. в нашей [документации по переносу][migration documentation].</span><span class="sxs-lookup"><span data-stu-id="c1314-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="c1314-123">Созданный отчет можно сохранить и открыть в программе Excel.</span><span class="sxs-lookup"><span data-stu-id="c1314-123">After the report is generated you will be able to save and open the report in Excel.</span></span>

<span data-ttu-id="c1314-124">Обратите внимание, что при создании схемы миграции большинство проблем, определенных как «Объект», будут устранены, что позволит немедленно выполнить миграцию соответствующих данных.</span><span class="sxs-lookup"><span data-stu-id="c1314-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span></span> <span data-ttu-id="c1314-125">Просмотрите изменения, чтобы убедиться, что перед применением схемы не требуются дополнительные корректировки.</span><span class="sxs-lookup"><span data-stu-id="c1314-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="c1314-126">Перенос схемы</span><span class="sxs-lookup"><span data-stu-id="c1314-126">Migrate schema</span></span>
<span data-ttu-id="c1314-127">После подключения выберите «Перенести схему», чтобы создать сценарий переноса схемы для выбранных таблиц.</span><span class="sxs-lookup"><span data-stu-id="c1314-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span></span> <span data-ttu-id="c1314-128">Этот сценарий переносит структуру таблицы, приводит несовместимые типы данных в более совместимые формы и создает учетные данные безопасности и схему, если это указано пользователем в настройках миграции.</span><span class="sxs-lookup"><span data-stu-id="c1314-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span></span> <span data-ttu-id="c1314-129">Этот код можно запустить для целевого экземпляра хранилища данных SQL, сохранить в файл, скопировать в буфер обмена или даже отредактировать на месте, прежде чем выполнять дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="c1314-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="c1314-130">Как отмечалось выше, при переносе схемы следует просмотреть изменения, внесенные средством миграции, чтобы убедиться, что вы полностью понимаете их.</span><span class="sxs-lookup"><span data-stu-id="c1314-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="c1314-131">Перенос данных</span><span class="sxs-lookup"><span data-stu-id="c1314-131">Migrate data</span></span>
<span data-ttu-id="c1314-132">Выбрав команду «Перенести данные», можно создать сценарии BCP, которые переместят ваши данные сначала в неструктурированные файлы на сервере, а затем непосредственно в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c1314-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="c1314-133">Этот процесс рекомендуется использовать при перемещении небольших объемов данных. Поскольку повторные попытки не предусмотрены, необходимо учитывать возможность сбоев из-за нарушений работы сети.</span><span class="sxs-lookup"><span data-stu-id="c1314-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span></span> <span data-ttu-id="c1314-134">Для запуска этой процедуры необходимо установить служебную программу командной строки BCP. Схема для данных уже должна быть создана.</span><span class="sxs-lookup"><span data-stu-id="c1314-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span></span>

<span data-ttu-id="c1314-135">После заполнения указанных выше параметров нужно просто нажать кнопку запуска миграции, и в указанном расположении будет создан набор из двух пакетов.</span><span class="sxs-lookup"><span data-stu-id="c1314-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span></span> <span data-ttu-id="c1314-136">Запустите файл экспорта, чтобы экспортировать данные из источника миграции в неструктурированные файлы. Затем запустите файл импорта, чтобы импортировать данные в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c1314-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1314-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1314-137">Next steps</span></span>
<span data-ttu-id="c1314-138">Теперь, когда вы перенесли данные, ознакомьтесь с процессом [разработки][develop].</span><span class="sxs-lookup"><span data-stu-id="c1314-138">Now that you've migrated some data, check out how to [develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
