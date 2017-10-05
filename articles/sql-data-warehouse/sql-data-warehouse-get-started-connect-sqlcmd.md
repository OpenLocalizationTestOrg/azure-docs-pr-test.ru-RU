---
title: "Подключение к хранилищу данных SQL Azure (sqlcmd) | Документация Майкрософт"
description: "Подключайтесь к хранилищу данных SQL Azure и создавайте запросы к нему с помощью служебной программы командной строки [sqlcmd][sqlcmd]."
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
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="cd72d-103">Подключение к хранилищу данных SQL с помощью sqlcmd</span><span class="sxs-lookup"><span data-stu-id="cd72d-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd72d-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="cd72d-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="cd72d-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="cd72d-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="cd72d-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd72d-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="cd72d-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="cd72d-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="cd72d-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="cd72d-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="cd72d-109">Подключайтесь к хранилищу данных SQL Azure и создавайте запросы к нему с помощью служебной программы командной строки [sqlcmd][sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="cd72d-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="cd72d-110">1. Подключение</span><span class="sxs-lookup"><span data-stu-id="cd72d-110">1. Connect</span></span>
<span data-ttu-id="cd72d-111">Чтобы начать использовать [sqlcmd][sqlcmd], откройте командную строку и введите **sqlcmd** и строку подключения к базе данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd72d-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="cd72d-112">В строке подключения обязательно укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="cd72d-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="cd72d-113">**Server (-S)** — сервер в формате `<`имя_сервера`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="cd72d-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="cd72d-114">**Database (-D)** — имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="cd72d-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="cd72d-115">**Enable Quoted Identifiers (-I)** — для подключения к экземпляру хранилища данных SQL необходимо включить заключенные в кавычки идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="cd72d-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="cd72d-116">Чтобы использовать проверку подлинности SQL Server, необходимо добавить параметры имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="cd72d-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="cd72d-117">**User (-U)** — пользователь сервера в формате `<`Пользователь`>`.</span><span class="sxs-lookup"><span data-stu-id="cd72d-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="cd72d-118">**Password (-P)** — пароль, связанный с пользователем.</span><span class="sxs-lookup"><span data-stu-id="cd72d-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="cd72d-119">Например, строка подключения может выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="cd72d-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="cd72d-120">Чтобы использовать встроенную проверку подлинности Azure Active Directory, необходимо добавить параметры Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd72d-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="cd72d-121">**Проверки подлинности Azure Active Directory (-G):** — использовать Azure Active Directory для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="cd72d-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="cd72d-122">Например, строка подключения может выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="cd72d-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="cd72d-123">Необходимо [включить проверку подлинности Azure Active Directory](sql-data-warehouse-authentication.md) , чтобы выполнять проверку подлинности с помощью Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd72d-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="cd72d-124">2) Запрос</span><span class="sxs-lookup"><span data-stu-id="cd72d-124">2. Query</span></span>
<span data-ttu-id="cd72d-125">После подключения можно подавать любые поддерживаемые инструкции Transact-SQL для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="cd72d-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="cd72d-126">В этом примере запросы отправляются в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="cd72d-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="cd72d-127">В следующих примерах показано, как выполнить запросы в пакетном режиме, используя параметр -Q или передав SQL программе sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="cd72d-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="cd72d-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd72d-128">Next steps</span></span>
<span data-ttu-id="cd72d-129">Дополнительные сведения о параметрах, доступных в sqlcmd, см. в [документации по sqlcmd][sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="cd72d-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
