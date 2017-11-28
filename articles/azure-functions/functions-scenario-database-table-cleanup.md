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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="a2c62-103">Использовать функции Azure tooconnect tooan базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a2c62-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="a2c62-104">В этом разделе показано, как toocreate функции Azure toouse запланированного задания очищает строк в таблице в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c62-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="a2c62-105">новый Hello функции C# создается на основе шаблона триггера предварительно определенных таймера в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c62-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="a2c62-106">toosupport этот сценарий также необходимо задать строку подключения базы данных как параметр в приложение функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="a2c62-107">В этом сценарии используется массовой операции с базой данных hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="a2c62-108">toohave вашей функция процесс отдельных операций CRUD в таблице мобильные приложения, следует использовать [привязки мобильные приложения](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a2c62-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2c62-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a2c62-109">Prerequisites</span></span>

+ <span data-ttu-id="a2c62-110">В этой статье используется функция, активируемая по таймеру.</span><span class="sxs-lookup"><span data-stu-id="a2c62-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="a2c62-111">Полный hello шаги в разделе hello [создать функцию в Azure, запустившей таймер](functions-create-scheduled-function.md) toocreate на языке C# версии этой функции.</span><span class="sxs-lookup"><span data-stu-id="a2c62-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="a2c62-112">В этом разделе демонстрируется команду Transact-SQL, которая выполняет операции очистки массового в hello **SalesOrderHeader** таблицы в образце базы данных AdventureWorksLT hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="a2c62-113">toocreate hello учебной базой данных AdventureWorksLT, полный hello шаги в разделе hello [создать базу данных Azure SQL в hello портал Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2c62-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="a2c62-114">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="a2c62-114">Get connection information</span></span>

<span data-ttu-id="a2c62-115">Строка подключения hello tooget нужна для hello базы данных, созданного во время выполнения [создать базу данных Azure SQL в hello портал Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2c62-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="a2c62-116">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a2c62-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="a2c62-117">Выберите **баз данных SQL** hello левом меню и выберите базу данных по hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="a2c62-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="a2c62-118">Выберите **Показать строки подключения базы данных** и копирования hello завершения **ADO.NET** строку подключения.</span><span class="sxs-lookup"><span data-stu-id="a2c62-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Скопируйте строку подключения ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="a2c62-120">Задание строки подключения hello</span><span class="sxs-lookup"><span data-stu-id="a2c62-120">Set hello connection string</span></span> 

<span data-ttu-id="a2c62-121">Функция приложение размещает hello выполнение функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c62-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="a2c62-122">Это наиболее строки подключения toostore рекомендаций и другие секретные данные в функции настройки параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="a2c62-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="a2c62-123">При использовании параметров приложения не случайного раскрытия hello строки подключения в коде.</span><span class="sxs-lookup"><span data-stu-id="a2c62-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="a2c62-124">Перейдите tooyour функции приложения, созданного [создать функцию в Azure, запустившей таймер](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="a2c62-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="a2c62-125">Выберите **Функции платформы** > **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2c62-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Параметры приложения для приложения функции hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="a2c62-127">Прокрутите список вниз слишком**строки подключения** и добавьте строку подключения, используя параметры hello, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Добавление параметров приложения функции toohello строку соединения.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="a2c62-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="a2c62-129">Setting</span></span>       | <span data-ttu-id="a2c62-130">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="a2c62-130">Suggested value</span></span> | <span data-ttu-id="a2c62-131">Описание</span><span class="sxs-lookup"><span data-stu-id="a2c62-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="a2c62-132">**Имя**</span><span class="sxs-lookup"><span data-stu-id="a2c62-132">**Name**</span></span>  |  <span data-ttu-id="a2c62-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="a2c62-133">sqldb_connection</span></span>  | <span data-ttu-id="a2c62-134">Используется tooaccess hello хранятся строки подключения в коде функции.</span><span class="sxs-lookup"><span data-stu-id="a2c62-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="a2c62-135">**Значение**</span><span class="sxs-lookup"><span data-stu-id="a2c62-135">**Value**</span></span> | <span data-ttu-id="a2c62-136">Скопированная строка</span><span class="sxs-lookup"><span data-stu-id="a2c62-136">Copied string</span></span>  | <span data-ttu-id="a2c62-137">За строку hello подключения вы скопировали в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="a2c62-138">**Тип**</span><span class="sxs-lookup"><span data-stu-id="a2c62-138">**Type**</span></span> | <span data-ttu-id="a2c62-139">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="a2c62-139">SQL Database</span></span> | <span data-ttu-id="a2c62-140">Используйте подключение к базе данных SQL по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="a2c62-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a2c62-141">Click **Save**.</span></span>

<span data-ttu-id="a2c62-142">Теперь можно добавить hello C# функции кода, который подключается tooyour базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a2c62-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="a2c62-143">Обновление кода функции</span><span class="sxs-lookup"><span data-stu-id="a2c62-143">Update your function code</span></span>

1. <span data-ttu-id="a2c62-144">В приложении функции выберите функцию запуска таймера hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="a2c62-145">Добавьте следующие ссылки на сборки вверху hello hello существующий код функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="a2c62-146">Добавьте следующее hello `using` функция toohello инструкции:</span><span class="sxs-lookup"><span data-stu-id="a2c62-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="a2c62-147">Заменить существующий hello **запуска** функцию с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="a2c62-147">Replace hello existing **Run** function with hello following code:</span></span>
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

    <span data-ttu-id="a2c62-148">Команда в этом примере обновляет hello **состояние** столбец, основанный на дату отгрузки hello.</span><span class="sxs-lookup"><span data-stu-id="a2c62-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="a2c62-149">Он должен обновить 32 строки данных.</span><span class="sxs-lookup"><span data-stu-id="a2c62-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="a2c62-150">Нажмите кнопку **Сохранить**, Контрольные значения hello **журналы** windows для hello рядом функцию выполнения, то Обратите внимание hello число строк, обновленных в hello **SalesOrderHeader** таблицы.</span><span class="sxs-lookup"><span data-stu-id="a2c62-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Просмотр журналов функций hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="a2c62-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2c62-152">Next steps</span></span>

<span data-ttu-id="a2c62-153">Затем вам потребуется узнать функционирование toouse toointegrate логики приложения с другими службами.</span><span class="sxs-lookup"><span data-stu-id="a2c62-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a2c62-154">Создание функции, интегрируемой с Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a2c62-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="a2c62-155">Дополнительные сведения о функциях см. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="a2c62-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="a2c62-156">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="a2c62-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="a2c62-157">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="a2c62-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="a2c62-158">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a2c62-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="a2c62-159">(Тестирование функций Azure) Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="a2c62-159">Describes various tools and techniques for testing your functions.</span></span>  
