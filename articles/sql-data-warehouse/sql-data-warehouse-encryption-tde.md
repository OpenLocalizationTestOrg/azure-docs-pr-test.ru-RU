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
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL
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
tooenable прозрачное шифрование данных для хранилища данных SQL, выполните следующие действия hello.

1. Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)
2. В колонке базы данных hello, щелкните hello **параметры** кнопки
3. Выберите hello **прозрачное шифрование данных** параметр![][1]
4. Выберите hello **на** параметр![][2]
5. Щелкните **Сохранить**
   ![][3].  

## <a name="disabling-encryption"></a>Отключение шифрования
toodisable прозрачное шифрование данных для хранилища данных SQL, выполните следующие действия hello.

1. Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)
2. В колонке базы данных hello, щелкните hello **параметры** кнопки
3. Выберите hello **прозрачное шифрование данных** параметр![][1]
4. Выберите hello **Off** параметр![][4]
5. Щелкните **Сохранить**
   ![][5].  

## <a name="encryption-dmvs"></a>Динамические административные представления шифрования
Шифрование может быть подтверждена с hello следующие динамические административные представления:

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

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
