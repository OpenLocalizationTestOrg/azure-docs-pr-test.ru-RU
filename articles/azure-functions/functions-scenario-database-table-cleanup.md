---
title: "Выполнение задачи очистки базы данных с помощью Функций Azure | Документы Майкрософт"
description: "С помощью Функций Azure можно запланировать задачу, которая периодически подключается к базе данных SQL Azure для очистки строк."
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="84d9b-103">Подключение к базе данных SQL Azure с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="84d9b-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="84d9b-104">В этой статье показано, как с помощью Функций Azure создать запланированное задание, которое очищает строки в таблице базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84d9b-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="84d9b-105">Новая функция C# создается на основе стандартного шаблона триггера на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="84d9b-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="84d9b-106">Для выполнения этого сценария необходимо также задать строку подключения к базе данных как параметр в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="84d9b-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="84d9b-107">В этом сценарии к базе данных применяется массовая операция.</span><span class="sxs-lookup"><span data-stu-id="84d9b-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="84d9b-108">Чтобы функция обрабатывала отдельные операции CRUD в таблице мобильных приложений, следует использовать [привязки мобильных приложений](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="84d9b-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84d9b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84d9b-109">Prerequisites</span></span>

+ <span data-ttu-id="84d9b-110">В этой статье используется функция, активируемая по таймеру.</span><span class="sxs-lookup"><span data-stu-id="84d9b-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="84d9b-111">Чтобы создать версию этой функции на языке C#, выполните инструкции в статье [Создание в Azure функции, активируемой по таймеру](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="84d9b-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="84d9b-112">В этом разделе демонстрируется команда Transact-SQL, которая выполняет операцию массовой очистки в таблице **SalesOrderHeader** образца базы данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="84d9b-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="84d9b-113">Чтобы создать образец базы данных AdventureWorksLT, выполните инструкции в статье [Создание базы данных SQL Azure на портале Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84d9b-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="84d9b-114">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="84d9b-114">Get connection information</span></span>

<span data-ttu-id="84d9b-115">Необходимо получить строку подключения к базе данных, созданную при выполнении инструкций в статье [Создание базы данных SQL Azure на портале Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84d9b-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="84d9b-116">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="84d9b-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="84d9b-117">В меню слева выберите пункт **Базы данных SQL** и на странице **Базы данных SQL** выберите имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="84d9b-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="84d9b-118">Щелкните **Показать строки подключения к базам данных** и полностью скопируйте строку подключения **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="84d9b-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Скопируйте строку подключения ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="84d9b-120">Задание строки подключения</span><span class="sxs-lookup"><span data-stu-id="84d9b-120">Set the connection string</span></span> 

<span data-ttu-id="84d9b-121">Выполнение функций в Azure происходит с помощью приложения функций.</span><span class="sxs-lookup"><span data-stu-id="84d9b-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="84d9b-122">Рекомендуется хранить строки подключения и другие секретные данные в параметрах приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="84d9b-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="84d9b-123">Использование параметров приложения позволяет предотвратить случайное раскрытие строки подключения в коде.</span><span class="sxs-lookup"><span data-stu-id="84d9b-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="84d9b-124">Перейдите к приложению-функции, созданному в результате выполнения инструкций в статье [Создание в Azure функции, активируемой по таймеру](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="84d9b-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="84d9b-125">Выберите **Функции платформы** > **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="84d9b-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Параметры приложения-функции](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="84d9b-127">Прокрутите страницу вниз до раздела **Строки подключения** и добавьте строку подключения, используя параметры, указанные в таблице.</span><span class="sxs-lookup"><span data-stu-id="84d9b-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Добавьте строку подключения в параметры приложения-функции.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="84d9b-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="84d9b-129">Setting</span></span>       | <span data-ttu-id="84d9b-130">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="84d9b-130">Suggested value</span></span> | <span data-ttu-id="84d9b-131">Описание</span><span class="sxs-lookup"><span data-stu-id="84d9b-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="84d9b-132">**Имя**</span><span class="sxs-lookup"><span data-stu-id="84d9b-132">**Name**</span></span>  |  <span data-ttu-id="84d9b-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="84d9b-133">sqldb_connection</span></span>  | <span data-ttu-id="84d9b-134">Используется для доступа к сохраненной строке подключения в коде функции.</span><span class="sxs-lookup"><span data-stu-id="84d9b-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="84d9b-135">**Значение**</span><span class="sxs-lookup"><span data-stu-id="84d9b-135">**Value**</span></span> | <span data-ttu-id="84d9b-136">Скопированная строка</span><span class="sxs-lookup"><span data-stu-id="84d9b-136">Copied string</span></span>  | <span data-ttu-id="84d9b-137">Вставьте строку подключения, скопированную в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="84d9b-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="84d9b-138">**Тип**</span><span class="sxs-lookup"><span data-stu-id="84d9b-138">**Type**</span></span> | <span data-ttu-id="84d9b-139">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="84d9b-139">SQL Database</span></span> | <span data-ttu-id="84d9b-140">Используйте подключение к базе данных SQL по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="84d9b-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="84d9b-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="84d9b-141">Click **Save**.</span></span>

<span data-ttu-id="84d9b-142">Теперь можно добавить код функции C#, который подключается к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="84d9b-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="84d9b-143">Обновление кода функции</span><span class="sxs-lookup"><span data-stu-id="84d9b-143">Update your function code</span></span>

1. <span data-ttu-id="84d9b-144">В приложении-функции выберите функцию, активируемую по таймеру.</span><span class="sxs-lookup"><span data-stu-id="84d9b-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="84d9b-145">Добавьте следующие ссылки на сборки в начало существующего кода функции:</span><span class="sxs-lookup"><span data-stu-id="84d9b-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="84d9b-146">Добавьте в функцию следующие операторы `using` :</span><span class="sxs-lookup"><span data-stu-id="84d9b-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="84d9b-147">Замените имеющуюся функцию **Run** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="84d9b-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="84d9b-148">Этот пример команды обновляет значения в столбце **Состояние** в соответствии с датой отгрузки.</span><span class="sxs-lookup"><span data-stu-id="84d9b-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="84d9b-149">Он должен обновить 32 строки данных.</span><span class="sxs-lookup"><span data-stu-id="84d9b-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="84d9b-150">Нажмите кнопку **Сохранить**. Выполнение следующей функции можно просмотреть в окне **Журналы**. Запишите число строк, обновленных в таблице **SalesOrderHeader**.</span><span class="sxs-lookup"><span data-stu-id="84d9b-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Просмотрите журналы функции.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="84d9b-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84d9b-152">Next steps</span></span>

<span data-ttu-id="84d9b-153">Узнайте, как использовать Функции с Logic Apps для интеграции с другими службами.</span><span class="sxs-lookup"><span data-stu-id="84d9b-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="84d9b-154">Создание функции, интегрируемой с Logic Apps</span><span class="sxs-lookup"><span data-stu-id="84d9b-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="84d9b-155">Дополнительные сведения о Функциях см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="84d9b-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="84d9b-156">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="84d9b-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="84d9b-157">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="84d9b-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="84d9b-158">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="84d9b-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="84d9b-159">(Тестирование функций Azure) Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="84d9b-159">Describes various tools and techniques for testing your functions.</span></span>  
