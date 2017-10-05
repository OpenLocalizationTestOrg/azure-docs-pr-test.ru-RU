---
title: "Прозрачное шифрование данных в хранилище данных SQL (T-SQL) | Документация Майкрософт"
description: "Прозрачное шифрование данных в хранилище данных SQL (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="792aa-103">Начало работы с прозрачным шифрованием данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="792aa-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="792aa-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="792aa-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="792aa-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="792aa-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="792aa-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="792aa-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="792aa-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="792aa-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="792aa-108">Необходимые права</span><span class="sxs-lookup"><span data-stu-id="792aa-108">Required Permssions</span></span>
<span data-ttu-id="792aa-109">Чтобы включить прозрачное шифрование данных, необходимо иметь права администратора или участника роли dbmanager.</span><span class="sxs-lookup"><span data-stu-id="792aa-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="792aa-110">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="792aa-110">Enabling Encryption</span></span>
<span data-ttu-id="792aa-111">Чтобы включить прозрачное шифрование данных для хранилища данных SQL, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="792aa-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="792aa-112">Подключитесь к *главной* базе данных на сервере, где находится база данных, указав логин администратора или члена роли **dbmanager** в главной базе данных.</span><span class="sxs-lookup"><span data-stu-id="792aa-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="792aa-113">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="792aa-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="792aa-114">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="792aa-114">Disabling Encryption</span></span>
<span data-ttu-id="792aa-115">Чтобы отключить прозрачное шифрование данных для хранилища данных SQL, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="792aa-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="792aa-116">Подключитесь к *главной* базе данных, указав логин администратора или члена роли **dbmanager** в главной базе данных.</span><span class="sxs-lookup"><span data-stu-id="792aa-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="792aa-117">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="792aa-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="792aa-118">Прежде чем вносить изменения в параметры прозрачного шифрования данных, работу приостановленного хранилища данных SQL нужно возобновить.</span><span class="sxs-lookup"><span data-stu-id="792aa-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="792aa-119">Проверка шифрования</span><span class="sxs-lookup"><span data-stu-id="792aa-119">Verifying Encryption</span></span>
<span data-ttu-id="792aa-120">Чтобы проверить состояние шифрования для хранилища данных SQL, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="792aa-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="792aa-121">Подключитесь к *главной* базе данных или к экземпляру базы данных, указав логин администратора или члена роли **dbmanager** в главной базе данных.</span><span class="sxs-lookup"><span data-stu-id="792aa-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="792aa-122">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="792aa-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="792aa-123">Результат ```1``` означает зашифрованную, а ```0``` — незашифрованную базу данных.</span><span class="sxs-lookup"><span data-stu-id="792aa-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="792aa-124">Динамические административные представления шифрования</span><span class="sxs-lookup"><span data-stu-id="792aa-124">Encryption DMVs</span></span>
* <span data-ttu-id="792aa-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="792aa-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="792aa-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="792aa-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
