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
# <a name="get-started-with-transparent-data-encryption-tde"></a>Начало работы с прозрачным шифрованием данных (TDE)
> [!div class="op_single_selector"]
> * [Обзор безопасности](sql-data-warehouse-overview-manage-security.md)
> * [Аутентификация](sql-data-warehouse-authentication.md)
> * [Шифрование (портал)](sql-data-warehouse-encryption-tde.md)
> * [Шифрование (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Необходимые права
tooenable прозрачное шифрование данных (TDE), необходимо быть администратором или членом роли dbmanager hello.

## <a name="enabling-encryption"></a>Включение шифрования
Выполните эти шаги tooenable прозрачное шифрование данных для хранилища данных SQL.

1. Подключение toohello *master* базы данных на сервере hello hello базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello
2. Выполнение hello, следующая инструкция tooencrypt hello, базы данных.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Отключение шифрования
Выполните эти шаги toodisable прозрачное шифрование данных для хранилища данных SQL.

1. Подключение toohello *master* базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello
2. Выполнение hello, следующая инструкция tooencrypt hello, базы данных.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Перед внесением изменений в параметры toohello прозрачного шифрования данных должна быть возобновлена приостановленной хранилища данных SQL.
> 
> 

## <a name="verifying-encryption"></a>Проверка шифрования
состояние шифрования tooverify для хранилища данных SQL, следуйте инструкциям hello:

1. Подключение toohello *master* или базы данных экземпляра, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello
2. Выполнение hello, следующая инструкция tooencrypt hello, базы данных.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Результат ```1``` означает зашифрованную, а ```0``` — незашифрованную базу данных.

## <a name="encryption-dmvs"></a>Динамические административные представления шифрования
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
