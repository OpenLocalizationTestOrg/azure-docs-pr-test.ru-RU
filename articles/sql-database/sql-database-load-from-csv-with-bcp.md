---
title: "aaaLoad данных из CSV-файла в базе данных SQL Azure (bcp) | Документы Microsoft"
description: "Для данных небольшого объема использует bcp tooimport данные в базу данных SQL Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Загрузка данных из CSV-файла в базу данных SQL Azure (неструктурированные файлы)
Можно использовать программы командной строки tooimport hello bcp данные из CSV-файла в базу данных SQL Azure.

## <a name="before-you-begin"></a>Перед началом работы
### <a name="prerequisites"></a>Предварительные требования
toocomplete hello шаги в этой статье, необходимо:

* Логический сервер и база данных SQL Azure
* Программа командной строки bcp Hello установлен
* Программа командной строки sqlcmd Hello установлен

Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Данные в формате ASCII или UTF-16
Если вы пытаетесь этот учебник с вашими собственными данными, данные требуют toouse hello ASCII или кодировку UTF-16, так как bcp поддерживает UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Создание целевой таблицы
Определение таблицы в базе данных SQL как hello целевой таблицы. Hello столбцов в таблице hello должно соответствовать toohello данных в каждой строке файла данных.

toocreate таблицу, откройте командную строку и использовать hello toorun sqlcmd.exe следующую команду:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a>2. Создание файла источника данных
Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt. Эти данные имеют формат ASCII.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Необязательно) tooexport данные из базы данных SQL Server, откройте командную строку и запустите следующую команду hello. Замените значения TableName, ServerName, DatabaseName, Username и Password на собственные.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Загрузка данных hello
tooload hello данных, откройте командную строку и запустите hello следующую команду, заменив своих собственных сведений значениями hello имя сервера, имя базы данных, имя пользователя и пароль.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Используйте эти данные hello tooverify команда была загружена неправильно

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Hello результаты должны выглядеть следующим образом:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="next-steps"></a>Дальнейшие действия
toomigrate базы данных SQL Server, в разделе [миграции баз данных SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
