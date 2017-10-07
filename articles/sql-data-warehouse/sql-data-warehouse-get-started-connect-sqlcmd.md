---
title: "Хранилище данных SQL sqlcmd aaaConnect tooAzure | Документы Microsoft"
description: "Используйте [sqlcmd] [sqlcmd] программы командной строки tooconnect tooand запрос хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Подключение tooSQL хранилища данных с помощью sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [машинное обучение Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Используйте [sqlcmd] [ sqlcmd] tooand tooconnect программы командной строки запроса в хранилище данных SQL Azure.  

## <a name="1-connect"></a>1. Подключение
tooget к работе с [sqlcmd][sqlcmd], откройте командную строку hello и введите **sqlcmd** следуют hello строку подключения для базы данных хранилища данных SQL. Строка подключения Hello требует hello следующие параметры:

* **Сервер (-S):** сервера в виде hello `<`имя сервера`>`. database.windows.net
* **Database (-D)** — имя базы данных.
* **Включить идентификаторы в кавычках (-я):** идентификаторы в кавычках должен быть включен tooconnect tooa хранилище данных SQL.

toouse проверки подлинности SQL Server необходимо имя пользователя и пароль параметры tooadd hello:

* **Пользователь (-U):** пользователя сервера в виде hello `<`пользователя`>`
* **Пароль (-P):** пароль, связанный с пользователем hello.

Например строка подключения может выглядеть hello следующее:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Azure Active Directory Integrated authentication toouse, необходимые параметры Azure Active Directory tooadd hello.

* **Проверки подлинности Azure Active Directory (-G):** — использовать Azure Active Directory для проверки подлинности.

Например строка подключения может выглядеть hello следующее:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> Требуется слишком[Включение проверки подлинности Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate, с помощью Active Directory.
> 
> 

## <a name="2-query"></a>2. Запрос
После подключения может выдавать любые поддерживаемые инструкции Transact-SQL, для экземпляра hello.  В этом примере запросы отправляются в интерактивном режиме.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Эти далее примерах процесса выполнения запросов в пакетном режиме с помощью параметра -Q hello или передачи на toosqlcmd SQL.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Дальнейшие действия
В разделе [документации sqlcmd] [ sqlcmd] Дополнительные сведения о дополнительных сведений о вариантах hello в sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
