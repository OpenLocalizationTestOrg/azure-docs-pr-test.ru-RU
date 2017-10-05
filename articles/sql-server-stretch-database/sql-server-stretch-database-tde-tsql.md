---
title: "Включение прозрачного шифрования данных для базы данных Stretch с помощью T-SQL в Azure | Документация Майкрософт"
description: "Включение прозрачного шифрования данных (TDE) для базы данных SQL Server Stretch в Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="41702-103">Включение прозрачного шифрования данных (TDE) для базы данных Stretch в Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="41702-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41702-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="41702-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="41702-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="41702-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="41702-106">Прозрачное шифрование данных (TDE) помогает защититься от угрозы вредоносных атак за счет шифрования и расшифровки базы данных, связанных резервных копий и файлов журналов транзакций при хранении в реальном времени, не внося изменения в само приложение.</span><span class="sxs-lookup"><span data-stu-id="41702-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="41702-107">При использовании TDE хранилище всей базы данных шифруется с помощью симметричного ключа, который называется ключом шифрования базы данных.</span><span class="sxs-lookup"><span data-stu-id="41702-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="41702-108">Ключ шифрования базы данных защищается встроенным сертификатом сервера.</span><span class="sxs-lookup"><span data-stu-id="41702-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="41702-109">Каждый сервер Azure обладает уникальным встроенным сертификатом.</span><span class="sxs-lookup"><span data-stu-id="41702-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="41702-110">Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней.</span><span class="sxs-lookup"><span data-stu-id="41702-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="41702-111">Общие сведения о прозрачном шифровании данных см. в [этой статье].</span><span class="sxs-lookup"><span data-stu-id="41702-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="41702-112">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="41702-112">Enabling Encryption</span></span>
<span data-ttu-id="41702-113">Чтобы включить прозрачное шифрование для базы данных Azure, где хранятся данные, перенесенные из Базы данных SQL Server Stretch, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="41702-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="41702-114">Подключитесь к базе данных *master* на сервере Azure, где находится база данных, указав имя входа администратора или члена роли **dbmanager** в базе данных master.</span><span class="sxs-lookup"><span data-stu-id="41702-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="41702-115">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="41702-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="41702-116">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="41702-116">Disabling Encryption</span></span>
<span data-ttu-id="41702-117">Чтобы отключить прозрачное шифрование для базы данных Azure, где хранятся данные, перенесенные из Базы данных SQL Server Stretch, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="41702-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="41702-118">Подключитесь к *главной* базе данных, указав логин администратора или члена роли **dbmanager** в главной базе данных.</span><span class="sxs-lookup"><span data-stu-id="41702-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="41702-119">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="41702-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="41702-120">Проверка шифрования</span><span class="sxs-lookup"><span data-stu-id="41702-120">Verifying Encryption</span></span>
<span data-ttu-id="41702-121">Чтобы проверить состояние шифрования для базы данных Azure, где хранятся данные, перенесенные из Базы данных SQL Server Stretch, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="41702-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="41702-122">Подключитесь к *главной* базе данных или к экземпляру базы данных, указав логин администратора или члена роли **dbmanager** в главной базе данных.</span><span class="sxs-lookup"><span data-stu-id="41702-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="41702-123">Выполните следующий оператор для шифрования базы данных:</span><span class="sxs-lookup"><span data-stu-id="41702-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="41702-124">Результат ```1``` означает зашифрованную, а ```0``` — незашифрованную базу данных.</span><span class="sxs-lookup"><span data-stu-id="41702-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="41702-125">[этой статье]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="41702-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
