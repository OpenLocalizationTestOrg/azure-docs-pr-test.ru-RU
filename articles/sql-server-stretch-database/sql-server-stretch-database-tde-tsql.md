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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Включение прозрачного шифрования данных (TDE) для базы данных Stretch в Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Портал Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Прозрачное шифрование данных (TDE) защищает от угроз вредоносных действий hello выполняя в реальном времени шифрование и расшифровку hello базы данных, связанных резервных копий и файлов журнала транзакций при этом не требуется toohello изменения приложение.

TDE шифрует hello хранения всей базы данных с помощью ключа шифрования симметричного ключа вызываемой hello базы данных. ключ шифрования базы данных Hello защищен используется встроенный сертификат сервера. Hello встроенный сертификат сервера уникален для каждого сервера Azure. Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней. Общие сведения о прозрачном шифровании данных см. в [этой статье].

## <a name="enabling-encryption"></a>Включение шифрования
tooenable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:

1. Подключение toohello *master* базы данных на hello Azure сервер размещения hello базы данных с помощью имени входа, которое является администратором или членом hello **dbmanager** роли в базе данных master hello
2. Выполнение hello, следующая инструкция tooencrypt hello, базы данных.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Отключение шифрования
toodisable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:

1. Подключение toohello *master* базы данных, используя учетные данные администратора или члена hello **dbmanager** роли в базе данных master hello
2. Выполнение hello, следующая инструкция tooencrypt hello, базы данных.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Проверка шифрования
tooverify состояние шифрования для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:

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

<!--Anchors-->
[этой статье]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
