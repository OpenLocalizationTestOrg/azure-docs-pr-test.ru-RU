---
title: "Хранилище данных SQL sqlcmd aaaConnect tooAzure | Документы Microsoft"
description: "Используйте [sqlcmd] [sqlcmd] программы командной строки tooconnect tooand запрос хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="7b53b-103">Подключение tooSQL хранилища данных с помощью sqlcmd</span><span class="sxs-lookup"><span data-stu-id="7b53b-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b53b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="7b53b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="7b53b-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="7b53b-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="7b53b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b53b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="7b53b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="7b53b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="7b53b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="7b53b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="7b53b-109">Используйте [sqlcmd] [ sqlcmd] tooand tooconnect программы командной строки запроса в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b53b-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="7b53b-110">1. Подключение</span><span class="sxs-lookup"><span data-stu-id="7b53b-110">1. Connect</span></span>
<span data-ttu-id="7b53b-111">tooget к работе с [sqlcmd][sqlcmd], откройте командную строку hello и введите **sqlcmd** следуют hello строку подключения для базы данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7b53b-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="7b53b-112">Строка подключения Hello требует hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7b53b-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="7b53b-113">**Сервер (-S):** сервера в виде hello `<`имя сервера`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="7b53b-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="7b53b-114">**Database (-D)** — имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="7b53b-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="7b53b-115">**Включить идентификаторы в кавычках (-я):** идентификаторы в кавычках должен быть включен tooconnect tooa хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7b53b-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="7b53b-116">toouse проверки подлинности SQL Server необходимо имя пользователя и пароль параметры tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="7b53b-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="7b53b-117">**Пользователь (-U):** пользователя сервера в виде hello `<`пользователя`>`</span><span class="sxs-lookup"><span data-stu-id="7b53b-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="7b53b-118">**Пароль (-P):** пароль, связанный с пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="7b53b-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="7b53b-119">Например строка подключения может выглядеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7b53b-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="7b53b-120">Azure Active Directory Integrated authentication toouse, необходимые параметры Azure Active Directory tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="7b53b-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="7b53b-121">**Проверки подлинности Azure Active Directory (-G):** — использовать Azure Active Directory для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7b53b-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="7b53b-122">Например строка подключения может выглядеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7b53b-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="7b53b-123">Требуется слишком[Включение проверки подлинности Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate, с помощью Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b53b-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="7b53b-124">2. Запрос</span><span class="sxs-lookup"><span data-stu-id="7b53b-124">2. Query</span></span>
<span data-ttu-id="7b53b-125">После подключения может выдавать любые поддерживаемые инструкции Transact-SQL, для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="7b53b-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="7b53b-126">В этом примере запросы отправляются в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="7b53b-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="7b53b-127">Эти далее примерах процесса выполнения запросов в пакетном режиме с помощью параметра -Q hello или передачи на toosqlcmd SQL.</span><span class="sxs-lookup"><span data-stu-id="7b53b-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="7b53b-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b53b-128">Next steps</span></span>
<span data-ttu-id="7b53b-129">В разделе [документации sqlcmd] [ sqlcmd] Дополнительные сведения о дополнительных сведений о вариантах hello в sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="7b53b-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
