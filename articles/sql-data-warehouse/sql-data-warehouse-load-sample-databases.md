---
title: "aaaLoad образца данных в хранилище данных SQL | Документы Microsoft"
description: "Загрузка образца данных в хранилище данных SQL"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Загрузка образца данных в хранилище данных SQL
Выполните эти простые действия tooload и запрос к базе данных Adventure Works образец hello. Сначала с помощью этих скриптов sqlcmd toorun SQL, что приведет к созданию таблиц и представлений. После создания таблицы bcp tooload данные будут использоваться в сценарии hello.  Если у вас еще нет sqlcmd и bcp установлена, перейдите по соответствующей ссылке слишком[установить bcp] [ install bcp] и слишком[установить sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Загрузка примера данных
1. Загрузите hello [Adventure Works примеры сценариев для хранилища данных SQL] [ Adventure Works Sample Scripts for SQL Data Warehouse] ZIP-файл.
2. Извлеките файлы hello из каталога tooa загруженный zip на локальном компьютере.
3. Измените aw_create.bat hello извлечь файл и задайте следующие переменные, найденные в начале hello файла hello hello.  Быть убедиться, что tooleave без пробелов между hello «=» и параметром hello.  Ниже приведены примеры того, как могут выглядеть такие изменения.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Запустите aw_create.bat изменить hello из командную строку Windows.  Убедитесь, что вы находитесь в каталоге hello, где был сохранен aw_create.bat вашей измененной версии.
   Вот что делает этот сценарий:
   
   * удаляет все представления и таблицы Adventure Works, которые уже существуют в базе данных;
   * Создание hello Adventure Works таблиц и представлений
   * загружает каждую таблицу Adventure Works с помощью bcp;
   * Проверка hello количество строк для каждой таблицы Adventure Works
   * собирает статистику по каждому столбцу для каждой таблицы Adventure Works.

## <a name="query-sample-data"></a>Запрос части данных для примера
После загрузки некоторых демонстрационных данных в хранилище данных SQL можно быстро выполнить несколько запросов.  toorun запроса, подключите tooyour вновь созданные базы данных Adventure Works в хранилища данных SQL Azure с помощью Visual Studio и SSDT, как описано в hello [запроса с помощью Visual Studio] [ query with Visual Studio] документа.

Пример простого выберите tooget инструкции все сведения о hello hello сотрудников:

```sql
SELECT * FROM DimEmployee;
```

Пример более сложный запрос с помощью конструкций, таких как toolook GROUP BY в hello Общая сумма всех продаж за каждый день.

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Пример инструкции SELECT с toofilter предложение WHERE out заказами до определенной даты.

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Хранилище данных SQL поддерживает почти все конструкции T-SQL, которые поддерживаются SQL Server.  Все различия описаны в нашей документации по [переносу кода][migrate code].

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы tootry вероятность некоторых запросов с образцами данных, узнать о возможностях слишком[разработки][develop], [загрузить][load], или [ Перенос] [ migrate] tooSQL хранилища данных.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
