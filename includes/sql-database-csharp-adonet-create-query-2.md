
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="9aff7-101">Пример программы C#</span><span class="sxs-lookup"><span data-stu-id="9aff7-101">C# program example</span></span>

<span data-ttu-id="9aff7-102">В следующих разделах этой статьи представлена программа C#, в которой используется ADO.NET для отправки инструкций Transact-SQL в базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9aff7-102">The next sections of this article present a C# program that uses ADO.NET to send Transact-SQL statements to the SQL database.</span></span> <span data-ttu-id="9aff7-103">Программа C# выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9aff7-103">The C# program performs the following actions:</span></span>

1. <span data-ttu-id="9aff7-104">[подключается к базе данных SQL с помощью ADO.NET](#cs_1_connect);</span><span class="sxs-lookup"><span data-stu-id="9aff7-104">[Connects to our SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="9aff7-105">[создает таблицы](#cs_2_createtables);</span><span class="sxs-lookup"><span data-stu-id="9aff7-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="9aff7-106">[заполняет таблицы данными, выполняя инструкции T-SQL INSERT](#cs_3_insert);</span><span class="sxs-lookup"><span data-stu-id="9aff7-106">[Populates the tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="9aff7-107">[обновляет данные с помощью соединения](#cs_4_updatejoin);</span><span class="sxs-lookup"><span data-stu-id="9aff7-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="9aff7-108">[удаляет данные с помощью соединения](#cs_5_deletejoin);</span><span class="sxs-lookup"><span data-stu-id="9aff7-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="9aff7-109">[выбирает данные с помощью соединения](#cs_6_selectrows);</span><span class="sxs-lookup"><span data-stu-id="9aff7-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="9aff7-110">разрывает подключение (с удалением всех временных таблиц из базы данных tempdb).</span><span class="sxs-lookup"><span data-stu-id="9aff7-110">Closes the connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="9aff7-111">Программа C# содержит:</span><span class="sxs-lookup"><span data-stu-id="9aff7-111">The C# program contains:</span></span>

- <span data-ttu-id="9aff7-112">код C# для подключения к базе данных;</span><span class="sxs-lookup"><span data-stu-id="9aff7-112">C# code to connect to the database.</span></span>
- <span data-ttu-id="9aff7-113">методы, которые возвращают исходный код T-SQL;</span><span class="sxs-lookup"><span data-stu-id="9aff7-113">Methods that return the T-SQL source code.</span></span>
- <span data-ttu-id="9aff7-114">два способа отправки кода T-SQL в базу данных.</span><span class="sxs-lookup"><span data-stu-id="9aff7-114">Two methods that submit the T-SQL to the database.</span></span>

#### <a name="to-compile-and-run"></a><span data-ttu-id="9aff7-115">Компиляция и запуск</span><span class="sxs-lookup"><span data-stu-id="9aff7-115">To compile and run</span></span>

<span data-ttu-id="9aff7-116">Программа C# логически является одним CS-файлом.</span><span class="sxs-lookup"><span data-stu-id="9aff7-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="9aff7-117">Но в нашем примере она физически разделена на несколько блоков кода для удобства просмотра и изучения каждого блока.</span><span class="sxs-lookup"><span data-stu-id="9aff7-117">But here the program is physically divided into several code blocks, to make each block easier to see and understand.</span></span> <span data-ttu-id="9aff7-118">Чтобы скомпилировать и запустить программу, выполните инструкции ниже.</span><span class="sxs-lookup"><span data-stu-id="9aff7-118">To compile and run this program, do the following:</span></span>

1. <span data-ttu-id="9aff7-119">Создайте проект C# в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9aff7-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="9aff7-120">Тип проекта должно быть *консоли* приложение из примерно следующая иерархия: **шаблоны** > **Visual C#** >  **Для классических настольных приложений Windows** > **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-120">The project type should be a *console* application, from something like the following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="9aff7-121">В файле **Program.cs** удалите небольшие строки кода в начале.</span><span class="sxs-lookup"><span data-stu-id="9aff7-121">In the file **Program.cs**, erase the small starter lines of code.</span></span>
3. <span data-ttu-id="9aff7-122">Скопируйте и вставьте в Program.cs каждый из следующих блоков в той же последовательности, в которой они приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="9aff7-122">Into Program.cs, copy and paste each of the following blocks, in the same sequence they are presented here.</span></span>
4. <span data-ttu-id="9aff7-123">В файле Program.cs измените указанные ниже значения в методе **Main**:</span><span class="sxs-lookup"><span data-stu-id="9aff7-123">In Program.cs, edit the following values in the **Main** method:</span></span>

   - <span data-ttu-id="9aff7-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="9aff7-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="9aff7-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="9aff7-125">**cd.UserID**</span></span>
   - <span data-ttu-id="9aff7-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="9aff7-126">**cb.Password**</span></span>
   - <span data-ttu-id="9aff7-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="9aff7-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="9aff7-128">Убедитесь, что на сборку **System.Data.dll** есть ссылка.</span><span class="sxs-lookup"><span data-stu-id="9aff7-128">Verify that the assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="9aff7-129">Для этого разверните узел **Ссылки** на панели **обозревателя решений**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-129">To verify, expand the **References** node in the **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="9aff7-130">Чтобы создать программу в Visual Studio, щелкните меню **Сборка**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-130">To build the program in Visual Studio, click the **Build** menu.</span></span>
7. <span data-ttu-id="9aff7-131">Чтобы запустить программу из Visual Studio, нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-131">To run the program from Visual Studio, click the **Start** button.</span></span> <span data-ttu-id="9aff7-132">Результаты отчета отображаются в окне cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="9aff7-132">The report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="9aff7-133">Вы можете отредактировать T-SQL, чтобы добавить начальные **#** к именам таблиц, чтобы они создавались как временные таблицы в **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-133">You have the option of editing the T-SQL to add a leading **#** to the table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="9aff7-134">Это удобно при демонстрации, когда тестовая база данных недоступна.</span><span class="sxs-lookup"><span data-stu-id="9aff7-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="9aff7-135">Временные таблицы автоматически удаляются при закрытии подключения.</span><span class="sxs-lookup"><span data-stu-id="9aff7-135">Temporary tables are deleted automatically when the connection closes.</span></span> <span data-ttu-id="9aff7-136">Во временных таблицах ключевые слова REFERENCES для внешних ключей не применяются.</span><span class="sxs-lookup"><span data-stu-id="9aff7-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="9aff7-137">Блок C# 1: подключение с помощью ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9aff7-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="9aff7-138">Далее</span><span class="sxs-lookup"><span data-stu-id="9aff7-138">Next</span></span>](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View the report output here, then press any key to end the program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-to-create-tables"></a><span data-ttu-id="9aff7-139">Блок C# 2: T-SQL для создания таблиц</span><span class="sxs-lookup"><span data-stu-id="9aff7-139">C# block 2: T-SQL to create tables</span></span>

- <span data-ttu-id="9aff7-140">[Назад](#cs_1_connect) &nbsp; / &nbsp; [Далее](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="9aff7-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="9aff7-141">Схема отношения элементов (ERD)</span><span class="sxs-lookup"><span data-stu-id="9aff7-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="9aff7-142">Предыдущие инструкции CREATE TABLE включают ключевое слово **REFERENCES** для создания отношения *внешнего ключа* (FK) между двумя таблицами.</span><span class="sxs-lookup"><span data-stu-id="9aff7-142">The preceding CREATE TABLE statements involve the **REFERENCES** keyword to create a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="9aff7-143">При использовании tempdb закомментируйте ключевое слово `--REFERENCES` с помощью пары начальных тире.</span><span class="sxs-lookup"><span data-stu-id="9aff7-143">If you are using tempdb, comment out the `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="9aff7-144">На следующей схеме ERD представлено отношение между двумя таблицами.</span><span class="sxs-lookup"><span data-stu-id="9aff7-144">Next is an ERD that displays the relationship between the two tables.</span></span> <span data-ttu-id="9aff7-145">Значения в *дочернем* столбце #tabEmployee.DepartmentCode ограничены значениями *родительского* столбца #tabDepartment.Department.</span><span class="sxs-lookup"><span data-stu-id="9aff7-145">The values in the #tabEmployee.DepartmentCode *child* column are limited to the values present in the #tabDepartment.Department *parent* column.</span></span>

![Схема ERD с внешним ключом](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-to-insert-data"></a><span data-ttu-id="9aff7-147">Блок C# 3: T-SQL для вставки данных</span><span class="sxs-lookup"><span data-stu-id="9aff7-147">C# block 3: T-SQL to insert data</span></span>

- <span data-ttu-id="9aff7-148">[Назад](#cs_2_createtables) &nbsp; / &nbsp; [Далее](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="9aff7-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- The company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- The company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-to-update-join"></a><span data-ttu-id="9aff7-149">Блок C# 4: T-SQL для обновления соединения</span><span class="sxs-lookup"><span data-stu-id="9aff7-149">C# block 4: T-SQL to update-join</span></span>

- <span data-ttu-id="9aff7-150">[Назад](#cs_3_insert) &nbsp; / &nbsp; [Далее](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="9aff7-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-to-delete-join"></a><span data-ttu-id="9aff7-151">Блок C# 5: T-SQL для удаления соединения</span><span class="sxs-lookup"><span data-stu-id="9aff7-151">C# block 5: T-SQL to delete-join</span></span>

- <span data-ttu-id="9aff7-152">[Назад](#cs_4_updatejoin) &nbsp; / &nbsp; [Далее](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="9aff7-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size the Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband the Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-to-select-rows"></a><span data-ttu-id="9aff7-153">Блок C# 6: T-SQL для выбора строк</span><span class="sxs-lookup"><span data-stu-id="9aff7-153">C# block 6: T-SQL to select rows</span></span>

- <span data-ttu-id="9aff7-154">[Назад](#cs_5_deletejoin) &nbsp; / &nbsp; [Далее](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="9aff7-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all the final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a><span data-ttu-id="9aff7-155">Блок C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="9aff7-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="9aff7-156">[Назад](#cs_6_selectrows) &nbsp; / &nbsp; [Далее](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="9aff7-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="9aff7-157">Этот метод предназначен для выполнения инструкции T-SQL SELECT, созданной методом **Build_6_Tsql_SelectEmployees**.</span><span class="sxs-lookup"><span data-stu-id="9aff7-157">This method is designed to run the T-SQL SELECT statement that is built by the **Build_6_Tsql_SelectEmployees** method.</span></span>


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="9aff7-158">Блок C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="9aff7-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="9aff7-159">[Назад](#cs_6b_datareader) &nbsp; / &nbsp; [Далее](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="9aff7-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="9aff7-160">Этот метод вызывается для операций, которые изменяют информационное содержимое таблиц, не возвращая строки данных.</span><span class="sxs-lookup"><span data-stu-id="9aff7-160">This method is called for operations that modify the data content of tables without returning any data rows.</span></span>


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL to {0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-to-the-console"></a><span data-ttu-id="9aff7-161">Блок C# 8: вывод фактических результатов тестирования на консоль</span><span class="sxs-lookup"><span data-stu-id="9aff7-161">C# block 8: Actual test output to the console</span></span>

- [<span data-ttu-id="9aff7-162">Назад</span><span class="sxs-lookup"><span data-stu-id="9aff7-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="9aff7-163">Этот раздел содержит результаты, отправленные программой на консоль.</span><span class="sxs-lookup"><span data-stu-id="9aff7-163">This section captures the output that the program sent to the console.</span></span> <span data-ttu-id="9aff7-164">Для разных тестовых запусков изменяются только значения guid.</span><span class="sxs-lookup"><span data-stu-id="9aff7-164">Only the guid values vary between test runs.</span></span>


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
