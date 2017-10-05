---
title: "Прозрачное шифрование данных в хранилище данных SQL (на портале) | Документация Майкрософт"
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
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="414e4-103">Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="414e4-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="414e4-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="414e4-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="414e4-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="414e4-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="414e4-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="414e4-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="414e4-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="414e4-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="414e4-108">Необходимые права</span><span class="sxs-lookup"><span data-stu-id="414e4-108">Required Permssions</span></span>
<span data-ttu-id="414e4-109">Чтобы включить прозрачное шифрование данных, необходимо иметь права администратора или участника роли dbmanager.</span><span class="sxs-lookup"><span data-stu-id="414e4-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="414e4-110">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="414e4-110">Enabling Encryption</span></span>
<span data-ttu-id="414e4-111">Чтобы включить прозрачное шифрование данных для хранилища данных SQL, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="414e4-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="414e4-112">Откройте базу данных на [портале Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="414e4-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="414e4-113">В колонке базы данных нажмите кнопку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="414e4-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="414e4-114">Выберите параметр **Прозрачное шифрование данных** . ![][1]</span><span class="sxs-lookup"><span data-stu-id="414e4-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="414e4-115">Выберите параметр **Вкл.** ![][2]</span><span class="sxs-lookup"><span data-stu-id="414e4-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="414e4-116">Щелкните **Сохранить**
   ![][3].</span><span class="sxs-lookup"><span data-stu-id="414e4-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="414e4-117">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="414e4-117">Disabling Encryption</span></span>
<span data-ttu-id="414e4-118">Чтобы отключить прозрачное шифрование данных для хранилища данных SQL, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="414e4-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="414e4-119">Откройте базу данных на [портале Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="414e4-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="414e4-120">В колонке базы данных нажмите кнопку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="414e4-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="414e4-121">Выберите параметр **Прозрачное шифрование данных** . ![][1]</span><span class="sxs-lookup"><span data-stu-id="414e4-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="414e4-122">Выберите параметр **Выкл.** ![][4]</span><span class="sxs-lookup"><span data-stu-id="414e4-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="414e4-123">Щелкните **Сохранить**
   ![][5].</span><span class="sxs-lookup"><span data-stu-id="414e4-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="414e4-124">Динамические административные представления шифрования</span><span class="sxs-lookup"><span data-stu-id="414e4-124">Encryption DMVs</span></span>
<span data-ttu-id="414e4-125">Шифрование может быть подтверждено с помощью следующих динамических административных представлений.</span><span class="sxs-lookup"><span data-stu-id="414e4-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="414e4-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="414e4-126">[sys.databases]</span></span>
* <span data-ttu-id="414e4-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="414e4-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="414e4-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="414e4-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="414e4-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="414e4-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
