---
title: "aaaManage группы баз данных Azure SQL | Документы Microsoft"
description: "Пошаговая инструкция по созданию задания эластичной базы данных и управлению им."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Создание развернутых баз данных SQL Azure и управление ими с помощью заданий обработки эластичных БД (предварительная версия)


**Задания обработки эластичных баз данных** упрощают управление группами баз данных, выполнение таких административных задач, как изменение схем, управление учетными данными, обновление эталонных данных, сбор данных о производительности или сбор данных телеметрии клиентов. Заданий эластичных баз данных в настоящее время доступна через портал Azure hello и командлеты PowerShell. Однако hello Azure портала предоставляет доступ к ограниченной функциональности ограниченный tooexecution среди всех баз данных в [эластичного пула (Предварительная версия)](sql-database-elastic-pool.md). задать дополнительные функции tooaccess и выполнение сценариев между несколькими базами данных, включая коллекцию пользовательских или сегмент (создан с помощью [клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-introduction.md)), в разделе [Создание и управление задания с помощью PowerShell](sql-database-elastic-jobs-powershell.md). Дополнительные сведения о заданиях см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).
* Пул эластичных баз данных. Ознакомьтесь с [пулами эластичных баз данных](sql-database-elastic-pool.md).
* Установка компонентов службы заданий обработки эластичных баз данных. В разделе [Установка hello эластичной базы данных задание службы](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Создание заданий
1. С помощью hello [портал Azure](https://portal.azure.com), из существующего пула эластичной базы данных задание, щелкните **создать задание**.
2. Введите hello имя пользователя и пароль администратора базы данных hello (созданные во время установки заданий) для базы данных управления заданиями hello (хранилище метаданных для заданий).
   
    ![Имя задания hello, введите или вставьте код и нажмите кнопку выполнения][1]
3. В hello **создать задание** колонки, введите имя для задания hello.
4. Введите hello пользователя имя и пароль tooconnect toohello целевой базы данных с разрешениями, достаточными для выполнения toosucceed сценария.
5. Вставьте или введите в скрипте hello T-SQL.
6. Щелкните **Сохранить**, а затем нажмите кнопку **Запустить**.
   
    ![Создание заданий и их выполнение][5]

## <a name="run-idempotent-jobs"></a>Запуск идемпотентных заданий
При выполнении сценария набор баз данных, необходимо убедиться, что hello скрипта является идемпотентной. То есть hello скрипт должен быть toorun может несколько раз, даже если он завершается сбоем перед незавершенной. Например, при сбое скрипта, задания hello автоматически повторит до ее успешного выполнения (в пределах, как "Повторить" hello логику со временем, перестанут Повтор hello). toodo способом Hello это предложение «IF EXISTS» toouse hello и удалить любой найден экземпляр перед созданием нового объекта. Ниже приведен пример.

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Или используйте предложение IF NOT EXISTS перед созданием нового экземпляра:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Затем этот скрипт обновляет hello таблицы, созданной ранее.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Проверка состояния заданий
После запуска задания вы можете проверить ход его выполнения.

1. На странице приветствия эластичного пула нажмите **управление заданиями**.
   
    ![Щелкните "Управление заданиями".][2]
2. Щелкните hello имя (a) задания. Hello **состояние** может быть «Завершено» или «Ошибка». сведения о задании Hello отображаются (b) с его дату и время создания и выполнения. Hello (c) ниже списке hello, показывающий ход выполнения hello hello скрипт для каждой базы данных в пуле hello, предоставления сведений о нем даты и времени.
   
    ![Проверка завершенного задания][3]

## <a name="checking-failed-jobs"></a>Проверка невыполненных заданий
Если происходит сбой задания, можно просмотреть журнал его выполнения. Щелкните имя hello toosee hello не удалось выполнить задание сведений о нем.

![Проверка невыполненного задания][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


