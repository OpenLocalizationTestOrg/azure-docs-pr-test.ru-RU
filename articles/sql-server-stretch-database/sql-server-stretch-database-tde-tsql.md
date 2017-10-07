---
title: "Прозрачное шифрование данных для растяжения базы данных TSQL - Azure aaaEnable | Документы Microsoft"
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
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="ca565-103">Включение прозрачного шифрования данных (TDE) для базы данных Stretch в Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ca565-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca565-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ca565-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="ca565-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="ca565-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="ca565-106">Прозрачное шифрование данных (TDE) защищает от угроз вредоносных действий hello выполняя в реальном времени шифрование и расшифровку hello базы данных, связанных резервных копий и файлов журнала транзакций при этом не требуется toohello изменения приложение.</span><span class="sxs-lookup"><span data-stu-id="ca565-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="ca565-107">TDE шифрует hello хранения всей базы данных с помощью ключа шифрования симметричного ключа вызываемой hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="ca565-108">ключ шифрования базы данных Hello защищен используется встроенный сертификат сервера.</span><span class="sxs-lookup"><span data-stu-id="ca565-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="ca565-109">Hello встроенный сертификат сервера уникален для каждого сервера Azure.</span><span class="sxs-lookup"><span data-stu-id="ca565-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="ca565-110">Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней.</span><span class="sxs-lookup"><span data-stu-id="ca565-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="ca565-111">Общие сведения о прозрачном шифровании данных см. в [этой статье].</span><span class="sxs-lookup"><span data-stu-id="ca565-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ca565-112">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="ca565-112">Enabling Encryption</span></span>
<span data-ttu-id="ca565-113">tooenable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca565-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ca565-114">Подключение toohello *master* базы данных на hello Azure сервер размещения hello базы данных с помощью имени входа, которое является администратором или членом hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="ca565-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="ca565-115">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="ca565-116">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="ca565-116">Disabling Encryption</span></span>
<span data-ttu-id="ca565-117">toodisable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca565-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ca565-118">Подключение toohello *master* базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="ca565-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="ca565-119">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="ca565-120">Проверка шифрования</span><span class="sxs-lookup"><span data-stu-id="ca565-120">Verifying Encryption</span></span>
<span data-ttu-id="ca565-121">tooverify состояние шифрования для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca565-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ca565-122">Подключение toohello *master* или базы данных экземпляра, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello</span><span class="sxs-lookup"><span data-stu-id="ca565-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="ca565-123">Выполнение hello, следующая инструкция tooencrypt hello, базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="ca565-124">Результат ```1``` означает зашифрованную, а ```0``` — незашифрованную базу данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[этой статье]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
