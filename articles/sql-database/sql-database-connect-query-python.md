---
title: "Использование Python для создания запросов к базе данных SQL Azure | Документация Майкрософт"
description: "В этой статье показано, как использовать Python для создания программы, которая подключается к базе данных SQL Azure, и создавать к ней запросы с помощью инструкций Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: On Demand
ms.tgt_pltfrm: n
ms.devlang: python
ms.topic: quickstart
ms.date: 08/09/2017
ms.author: carlrab
ms.openlocfilehash: f7496c7b78449d5ceae861dc0daac607acdb1f84
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/29/2017
---
# <a name="use-python-to-query-an-azure-sql-database"></a>Использование Python для создания запросов к базе данных SQL Azure

 В этом кратком руководстве показано, как использовать [Python](https://python.org) для подключения к базе данных SQL Azure, а затем с помощью инструкций Transact-SQL выполнить запрос данных.

## <a name="prerequisites"></a>Предварительные требования

Ниже указаны требования для работы с этим кратким руководством.

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

- [Правило брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) для общедоступного IP-адреса компьютера, на котором выполняются действия из этого краткого руководства.

- Убедитесь, что установлен компонент Python и связанное программное обеспечение для вашей операционной системы.

    - **Mac OS.** Установите Homebrew, Python, драйвер ODBC и SQLCMD, а затем драйвер Python для SQL Server. См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).
    - **Ubuntu.** Установите Python и другие необходимые пакеты, а затем установите драйвер Python для SQL Server. См. [шаги 1.2, 1.3 и 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).
    - **Windows.** Установите последнюю версию Python (переменная среды теперь настраивается автоматически), драйвер ODBC и SQLCMD, а затем установите драйвер Python для SQL Server. Ознакомьтесь с шагами 1.2, 1.3 и 2.1 в [этом руководстве](https://www.microsoft.com/sql-server/developer-get-started/python/windows/). 

## <a name="sql-server-connection-information"></a>Сведения о подключении SQL Server

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]
    
## <a name="insert-code-to-query-sql-database"></a>Вставка кода для отправки запроса к базе данных SQL 

1. Создайте файл **sqltest.py** в предпочитаемом текстовом редакторе.  

2. Замените содержимое следующим кодом и добавьте соответствующие значения для сервера, базы данных, пользователя и пароля.

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-the-code"></a>Выполнение кода

1. В командной строке выполните следующие команды:

   ```Python
   python sqltest.py
   ```

2. Убедитесь, что возвращены первые 20 строк, а затем закройте окно приложения.

## <a name="next-steps"></a>Дальнейшие действия

- [Проектирование первой базы данных SQL Azure](sql-database-design-first-database.md)
- [Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/) (Драйверы Microsoft Python для SQL Server)
- [Центр по разработке для Python](https://azure.microsoft.com/develop/python/?v=17.23h)

