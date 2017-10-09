
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>Пример программы C#

Hello далее разделах данной статьи представлены программы C#, который использует ADO.NET toosend Transact-SQL инструкции toohello базы данных SQL. Программа Hello C# выполняет hello, следующие действия:

1. [Подключается tooour базы данных SQL с помощью ADO.NET](#cs_1_connect).
2. [создает таблицы](#cs_2_createtables);
3. [Заполняет hello таблиц с данными, путем выполнения инструкций T-SQL INSERT](#cs_3_insert).
4. [обновляет данные с помощью соединения](#cs_4_updatejoin);
5. [удаляет данные с помощью соединения](#cs_5_deletejoin);
6. [выбирает данные с помощью соединения](#cs_6_selectrows);
7. Закрывает соединение hello (которая удаляет все временные таблицы из базы данных tempdb).

Программа Hello C# содержит:

- C# код tooconnect toohello базы данных.
- Методы, возвращающие исходного кода hello T-SQL.
- Два способа отправки базы данных toohello hello T-SQL.

#### <a name="toocompile-and-run"></a>toocompile и выполнения

Программа C# логически является одним CS-файлом. Но здесь программа hello физически разделить на несколько блоков кода, toomake каждый блок проще toosee и понять. toocompile и запустить программу, hello следующие:

1. Создайте проект C# в Visual Studio.
    - Тип проекта Hello следует *консоли* приложение из примерно следующая иерархия hello: **шаблоны** > **Visual C#** > **Windows классического** > **консольного приложения (.NET Framework)**.
3. В файле hello **Program.cs**, erase hello небольшой начальных строк кода.
3. В Program.cs копирования и вставки каждой hello в следующих блоках hello же последовательности, в котором они приведены ниже.
4. В Program.cs ниже hello редактирования значений в hello **Main** метод:

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. Проверить эту сборку hello **System.Data.dll** имеется ссылка. tooverify, разверните hello **ссылки** узел в hello **обозревателе решений** области.
6. Программа hello toobuild в Visual Studio щелкните hello **построения** меню.
7. Программа hello toorun из Visual Studio, щелкните hello **запустить** кнопки. в окне cmd.exe вывода отчетов Hello.

> [!NOTE]
> У вас есть возможность редактирования hello T-SQL tooadd символа hello  **#**  toohello имена таблиц, в которых будут созданы как временные таблицы в **tempdb**. Это удобно при демонстрации, когда тестовая база данных недоступна. Временные таблицы автоматически удаляются при закрытии соединения hello. Во временных таблицах ключевые слова REFERENCES для внешних ключей не применяются.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>Блок C# 1: подключение с помощью ADO.NET

- [Далее](#cs_2_createtables)


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
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>C# блок 2: toocreate таблицы T-SQL

- [Назад](#cs_1_connect) &nbsp; / &nbsp; [Далее](#cs_3_insert)

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

#### <a name="entity-relationship-diagram-erd"></a>Схема отношения элементов (ERD)

Hello предыдущие инструкции CREATE TABLE включают hello **ссылки** toocreate ключевое слово *внешний ключ* (FK) связь между двумя таблицами.  Если вы используете базы данных tempdb, закомментируйте hello `--REFERENCES` ключевое слово, с помощью пары начальные тире.

Далее следует диска аварийного восстановления, отображающий hello связь между двумя таблицами hello. Здравствуйте, значения в hello #tabEmployee.DepartmentCode *дочерних* столбца, ограниченного toohello значения, имеющиеся в hello #tabDepartment.Department *родительского* столбца.

![Схема ERD с внешним ключом](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>C# блокировку 3: tooinsert данных T-SQL

- [Назад](#cs_2_createtables) &nbsp; / &nbsp; [Далее](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
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
### <a name="c-block-4-t-sql-tooupdate-join"></a>C# блок 4: T-SQL tooupdate соединения

- [Назад](#cs_3_insert) &nbsp; / &nbsp; [Далее](#cs_5_deletejoin)


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
### <a name="c-block-5-t-sql-toodelete-join"></a>C# блок 5: T-SQL toodelete соединения

- [Назад](#cs_4_updatejoin) &nbsp; / &nbsp; [Далее](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>Блоке C# 6: tooselect строк T-SQL

- [Назад](#cs_5_deletejoin) &nbsp; / &nbsp; [Далее](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
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
### <a name="c-block-6b-executereader"></a>Блок C# 6b: ExecuteReader

- [Назад](#cs_6_selectrows) &nbsp; / &nbsp; [Далее](#cs_7_executenonquery)

Этот метод является спроектированный toorun hello T-SQL SELECT, построенного с hello **Build_6_Tsql_SelectEmployees** метод.


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
### <a name="c-block-7-executenonquery"></a>Блок C# 7: ExecuteNonQuery

- [Назад](#cs_6b_datareader) &nbsp; / &nbsp; [Далее](#cs_8_output)

Этот метод вызывается для операций, изменяющих hello содержимого данных таблиц, не возвращая все строки данных.


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
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

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
### <a name="c-block-8-actual-test-output-toohello-console"></a>C# блока 8: консоли toohello выходные данные теста

- [Назад](#cs_7_executenonquery)

Этот раздел содержит hello выходные данные, hello программы отправлено toohello консоли. Только значения guid hello различаться для разных тестовых запусков.


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
