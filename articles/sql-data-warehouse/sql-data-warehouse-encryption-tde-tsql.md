---
title: "Шифрование данных в хранилище данных SQL (T-SQL) aaaTransparent | Документы Microsoft"
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
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="abdf3-103">Начало работы с прозрачным шифрованием данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="abdf3-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abdf3-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="abdf3-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="abdf3-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="abdf3-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="abdf3-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="abdf3-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="abdf3-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="abdf3-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="abdf3-108">Необходимые права</span><span class="sxs-lookup"><span data-stu-id="abdf3-108">Required Permssions</span></span>
<span data-ttu-id="abdf3-109">tooenable прозрачное шифрование данных (TDE), необходимо быть администратором или членом роли dbmanager hello.</span><span class="sxs-lookup"><span data-stu-id="abdf3-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="abdf3-110">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="abdf3-110">Enabling Encryption</span></span>
<span data-ttu-id="abdf3-111">Выполните эти шаги tooenable прозрачное шифрование данных для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="abdf3-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="abdf3-112">Подключение toohello *master* базы данных на сервере hello hello базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="abdf3-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="abdf3-113">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="abdf3-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="abdf3-114">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="abdf3-114">Disabling Encryption</span></span>
<span data-ttu-id="abdf3-115">Выполните эти шаги toodisable прозрачное шифрование данных для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="abdf3-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="abdf3-116">Подключение toohello *master* базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="abdf3-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="abdf3-117">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="abdf3-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="abdf3-118">Перед внесением изменений в параметры toohello прозрачного шифрования данных должна быть возобновлена приостановленной хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="abdf3-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="abdf3-119">Проверка шифрования</span><span class="sxs-lookup"><span data-stu-id="abdf3-119">Verifying Encryption</span></span>
<span data-ttu-id="abdf3-120">состояние шифрования tooverify для хранилища данных SQL, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="abdf3-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="abdf3-121">Подключение toohello *master* или базы данных экземпляра, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="abdf3-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="abdf3-122">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="abdf3-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="abdf3-123">Результат ```1``` означает зашифрованную, а ```0``` — незашифрованную базу данных.</span><span class="sxs-lookup"><span data-stu-id="abdf3-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="abdf3-124">Динамические административные представления шифрования</span><span class="sxs-lookup"><span data-stu-id="abdf3-124">Encryption DMVs</span></span>
* <span data-ttu-id="abdf3-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="abdf3-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="abdf3-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="abdf3-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
