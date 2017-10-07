---
title: "Шифрование данных в хранилище данных SQL (портал) aaaTransparent | Документы Microsoft"
description: "Прозрачное шифрование данных в хранилище данных SQL на портале"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="44ac2-103">Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="44ac2-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44ac2-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="44ac2-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="44ac2-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="44ac2-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="44ac2-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="44ac2-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="44ac2-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="44ac2-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="44ac2-108">Необходимые права</span><span class="sxs-lookup"><span data-stu-id="44ac2-108">Required Permssions</span></span>
<span data-ttu-id="44ac2-109">tooenable прозрачное шифрование данных (TDE), необходимо быть администратором или членом роли dbmanager hello.</span><span class="sxs-lookup"><span data-stu-id="44ac2-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="44ac2-110">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="44ac2-110">Enabling Encryption</span></span>
<span data-ttu-id="44ac2-111">tooenable прозрачное шифрование данных для хранилища данных SQL, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="44ac2-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="44ac2-112">Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="44ac2-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="44ac2-113">В колонке базы данных hello, щелкните hello **параметры** кнопки</span><span class="sxs-lookup"><span data-stu-id="44ac2-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="44ac2-114">Выберите hello **прозрачное шифрование данных** параметр![][1]</span><span class="sxs-lookup"><span data-stu-id="44ac2-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="44ac2-115">Выберите hello **на** параметр![][2]</span><span class="sxs-lookup"><span data-stu-id="44ac2-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="44ac2-116">Щелкните **Сохранить**
   ![][3].</span><span class="sxs-lookup"><span data-stu-id="44ac2-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="44ac2-117">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="44ac2-117">Disabling Encryption</span></span>
<span data-ttu-id="44ac2-118">toodisable прозрачное шифрование данных для хранилища данных SQL, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="44ac2-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="44ac2-119">Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="44ac2-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="44ac2-120">В колонке базы данных hello, щелкните hello **параметры** кнопки</span><span class="sxs-lookup"><span data-stu-id="44ac2-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="44ac2-121">Выберите hello **прозрачное шифрование данных** параметр![][1]</span><span class="sxs-lookup"><span data-stu-id="44ac2-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="44ac2-122">Выберите hello **Off** параметр![][4]</span><span class="sxs-lookup"><span data-stu-id="44ac2-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="44ac2-123">Щелкните **Сохранить**
   ![][5].</span><span class="sxs-lookup"><span data-stu-id="44ac2-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="44ac2-124">Динамические административные представления шифрования</span><span class="sxs-lookup"><span data-stu-id="44ac2-124">Encryption DMVs</span></span>
<span data-ttu-id="44ac2-125">Шифрование может быть подтверждена с hello следующие динамические административные представления:</span><span class="sxs-lookup"><span data-stu-id="44ac2-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="44ac2-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="44ac2-126">[sys.databases]</span></span>
* <span data-ttu-id="44ac2-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="44ac2-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
