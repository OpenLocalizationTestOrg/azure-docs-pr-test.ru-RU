---
title: "Подключение tooAzure базы данных MySQL из рабочей среды MySQL | Документы Microsoft"
description: "Это краткое руководство предоставляет toouse действия hello MySQL Workbench tooconnect и запроса данных из базы данных Azure для MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>База данных Azure для MySQL: используйте MySQL Workbench tooconnect и запроса данных
Это краткое руководство демонстрирует, как tooan tooconnect базы данных Azure для использования MySQL hello приложения MySQL Workbench. 

## <a name="prerequisites"></a>Предварительные требования
Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)

## <a name="install-mysql-workbench"></a>Установка MySQL Workbench
Загрузите и установите на компьютер из рабочей среды MySQL [веб-сайта MySQL hello](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Получение сведений о подключении
Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL. Необходимо hello server полное имя и учетные данные входа.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).

2. Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **myserver4demo**.

3. Щелкните имя сервера hello.

4. Выберите hello server **свойства** страницы. Запишите hello **имя сервера** и **имя входа администратора сервера**.

 ![Имя сервера базы данных Azure для MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Подключиться с помощью MySQL Workbench server toohello 
с помощью средства hello графического интерфейса пользователя MySQL Workbench MySQL server tooAzure tooconnect:

1.  Запустите hello MySQL Workbench приложения на компьютере. 

2.  В **установки нового подключения** диалогового окна введите следующую информацию на hello hello **параметры** вкладки:

    ![Настройка нового подключения](./media/connect-workbench/2-setup-new-connection.png)

    | **Параметр** | **Рекомендуемое значение** | **Описание поля** |
    |---|---|---|
    |   Имя подключения | Пример подключения | Укажите метку для этого подключения. |
    | Способ подключения | Стандартный способ (по протоколу TCP/IP) | Стандартный способ (по протоколу TCP/IP) соответствует требованиям. |
    | имя узла; | *имя сервера* | Укажите значение имени сервера hello, который использовался при создании hello базы данных Azure для MySQL ранее. В нашем примере используется такое имя сервера: myserver4demo.mysql.database.azure.com. Используйте hello полное доменное имя (\*. mysql.database.azure.com) как показано в примере hello. Выполните действия hello hello предыдущего раздела tooget hello сведения о соединении, если вы не помните имя вашего сервера.  |
    | Порт | 3306 | Всегда используйте порт 3306 при подключении tooAzure базы данных MySQL. |
    | Имя пользователя |  *имя для входа администратора сервера* | Введите в hello входа имя входа администратора сервера указаны при создании hello базы данных Azure для MySQL ранее. Пример нашего имени пользователя — myadmin@myserver4demo. Выполните действия hello hello предыдущего раздела tooget hello сведения о соединении, если вы не помните hello имя пользователя. Формат Hello  *username@servername* .
    | Пароль | Ваш пароль. | Нажмите кнопку **хранилища в хранилище...**  кнопку toosave hello пароль. |

3.   Нажмите кнопку **проверить подключение** tootest, если все параметры настроены правильно. 

4.   Нажмите кнопку **ОК** toosave hello соединения. 

5.   В списке hello **подключений MySQL**выберите сервер tooyour соответствующие плитки hello и ожидания для установления toobe подключения hello.

6.   Откроется новая вкладка SQL с пустым окном редактора, в котором можно вводить запросы.

    > [!NOTE]
    > По умолчанию защита SSL-подключения является обязательной и применяется к базе данных Azure для сервера MySQL. Обычно для сервера tooyour tooconnect MySQL Workbench требуется дополнительная настройка с использованием сертификата SSL. Дополнительные сведения о протоколе SSL см. в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](./howto-configure-ssl.md).  При необходимости toodisable SSL посетите портал Azure hello и нажмите hello страница безопасности подключения toodisable hello переключателя подключения применять SSL кнопку.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Создание таблицы, добавление, считывание, обновление и удаление данных
1. Скопируйте и вставьте код SQL в образце hello в пустой tooillustrate вкладку SQL образцами данных.

    Этот код создает пустую базу данных с именем quickstartdb, а затем создает пример таблицы с именем inventory. Вставляет несколько строк, затем считывает строки hello. Он изменяет hello данных с помощью инструкции update и операций чтения hello строк еще раз. Наконец он удаляет строку и еще раз считывает строки hello.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    Снимок экрана приветствия показан пример hello кода SQL в SQL Workbench и hello выходных данных после его запуска.
    
    ![Вкладка SQL Workbench MySQL toorun пример кода SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. Образец hello toorun кода SQL, щелкните счет молнии панели инструментов hello hello hello **файл SQL** вкладки.
3. Обратите внимание, hello три результаты с вкладками в hello **сетки** раздел в середине hello страницы приветствия. 
4. Обратите внимание hello **вывода** списке hello нижней части страницы приветствия. отображается состояние Hello каждой команды. 

Теперь для MySQL с помощью MySQL Workbench подключились tooAzure базы данных и запросов данных с помощью языка SQL hello.

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Перенос базы данных с помощью экспорта и импорта](./concepts-migrate-import-export.md)
