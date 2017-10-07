---
title: "Функции Azure tooperform aaaUse базы данных очистки задач | Документы Microsoft"
description: "Использование функции Azure tooschedule задачу, которая подключается tooperiodically tooAzure базы данных SQL очистить строк."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Использовать функции Azure tooconnect tooan базы данных SQL Azure
В этом разделе показано, как toocreate функции Azure toouse запланированного задания очищает строк в таблице в базе данных SQL Azure. новый Hello функции C# создается на основе шаблона триггера предварительно определенных таймера в hello портал Azure. toosupport этот сценарий также необходимо задать строку подключения базы данных как параметр в приложение функции hello. В этом сценарии используется массовой операции с базой данных hello. toohave вашей функция процесс отдельных операций CRUD в таблице мобильные приложения, следует использовать [привязки мобильные приложения](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Предварительные требования

+ В этой статье используется функция, активируемая по таймеру. Полный hello шаги в разделе hello [создать функцию в Azure, запустившей таймер](functions-create-scheduled-function.md) toocreate на языке C# версии этой функции.   

+ В этом разделе демонстрируется команду Transact-SQL, которая выполняет операции очистки массового в hello **SalesOrderHeader** таблицы в образце базы данных AdventureWorksLT hello. toocreate hello учебной базой данных AdventureWorksLT, полный hello шаги в разделе hello [создать базу данных Azure SQL в hello портал Azure](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Получение сведений о подключении

Строка подключения hello tooget нужна для hello базы данных, созданного во время выполнения [создать базу данных Azure SQL в hello портал Azure](../sql-database/sql-database-get-started-portal.md).

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
 
3. Выберите **баз данных SQL** hello левом меню и выберите базу данных по hello **баз данных SQL** страницы.

4. Выберите **Показать строки подключения базы данных** и копирования hello завершения **ADO.NET** строку подключения.

    ![Скопируйте строку подключения ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Задание строки подключения hello 

Функция приложение размещает hello выполнение функций в Azure. Это наиболее строки подключения toostore рекомендаций и другие секретные данные в функции настройки параметров приложения. При использовании параметров приложения не случайного раскрытия hello строки подключения в коде. 

1. Перейдите tooyour функции приложения, созданного [создать функцию в Azure, запустившей таймер](functions-create-scheduled-function.md).

2. Выберите **Функции платформы** > **Параметры приложения**.
   
    ![Параметры приложения для приложения функции hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Прокрутите список вниз слишком**строки подключения** и добавьте строку подключения, используя параметры hello, как указано в таблице hello.
   
    ![Добавление параметров приложения функции toohello строку соединения.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Настройка       | Рекомендуемое значение | Описание             | 
    | ------------ | ------------------ | --------------------- | 
    | **Имя**  |  sqldb_connection  | Используется tooaccess hello хранятся строки подключения в коде функции.    |
    | **Значение** | Скопированная строка  | За строку hello подключения вы скопировали в предыдущем разделе hello. |
    | **Тип** | База данных SQL | Используйте подключение к базе данных SQL по умолчанию hello. |   

3. Щелкните **Сохранить**.

Теперь можно добавить hello C# функции кода, который подключается tooyour базы данных SQL.

## <a name="update-your-function-code"></a>Обновление кода функции

1. В приложении функции выберите функцию запуска таймера hello.
 
3. Добавьте следующие ссылки на сборки вверху hello hello существующий код функции hello.

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Добавьте следующее hello `using` функция toohello инструкции:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Заменить существующий hello **запуска** функцию с hello, следующий код:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Команда в этом примере обновляет hello **состояние** столбец, основанный на дату отгрузки hello. Он должен обновить 32 строки данных.

5. Нажмите кнопку **Сохранить**, Контрольные значения hello **журналы** windows для hello рядом функцию выполнения, то Обратите внимание hello число строк, обновленных в hello **SalesOrderHeader** таблицы.

    ![Просмотр журналов функций hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Дальнейшие действия

Затем вам потребуется узнать функционирование toouse toointegrate логики приложения с другими службами.

> [!div class="nextstepaction"] 
> [Создание функции, интегрируемой с Logic Apps](functions-twitter-email.md)

Дополнительные сведения о функциях см. в разделе hello следующие вопросы:

* [Справочник разработчика по функциям Azure](functions-reference.md)  
  Справочник программиста по созданию функций, а также определению триггеров и привязок.
* [Testing Azure Functions](functions-test-a-function.md)  
  (Тестирование функций Azure) Описание различных средств и методов тестирования функций.  
