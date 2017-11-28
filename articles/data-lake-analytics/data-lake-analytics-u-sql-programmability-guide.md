---
title: "Руководство по программированию U-SQL для Azure Data Lake | Документация Майкрософт"
description: "Узнайте о наборе служб в Azure Data Lake, позволяющих создать платформу больших данных на базе облака."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="a95c3-103">Руководство по программированию U-SQL</span><span class="sxs-lookup"><span data-stu-id="a95c3-103">U-SQL programmability guide</span></span>

<span data-ttu-id="a95c3-104">U-SQL — это специальный язык запросов для рабочих нагрузок, обрабатывающих большие данные.</span><span class="sxs-lookup"><span data-stu-id="a95c3-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="a95c3-105">U-SQL отличается использованием SQL-подобного декларативного синтаксиса, а также расширяемостью и удобством программирования, характерными для C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="a95c3-106">В этом руководстве мы рассмотрим расширяемость и программируемость языка U-SQL на основе C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="a95c3-107">Требования</span><span class="sxs-lookup"><span data-stu-id="a95c3-107">Requirements</span></span>

<span data-ttu-id="a95c3-108">Скачивание и установка [средств Azure Data Lake для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="a95c3-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="a95c3-109">Начало работы с U-SQL</span><span class="sxs-lookup"><span data-stu-id="a95c3-109">Get started with U-SQL</span></span>  

<span data-ttu-id="a95c3-110">Рассмотрим следующий скрипт U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a95c3-110">Let’s look at the following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="a95c3-111">Он определяет набор строк, который называется @a, и создает набор строк, который называется @results, из @a.</span><span class="sxs-lookup"><span data-stu-id="a95c3-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="a95c3-112">Типы и выражения C# в скрипте U-SQL</span><span class="sxs-lookup"><span data-stu-id="a95c3-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="a95c3-113">Выражение U-SQL — это выражение C# в сочетании с логическими операциями U-SQL, такими как `AND`, `OR`, и `NOT`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="a95c3-114">Выражения U-SQL можно использовать с инструкциями SELECT, EXTRACT, WHERE, HAVING, GROUP BY и DECLARE.</span><span class="sxs-lookup"><span data-stu-id="a95c3-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="a95c3-115">Например, следующий скрипт анализирует значение строки даты и времени (DateTime) в предложении SELECT.</span><span class="sxs-lookup"><span data-stu-id="a95c3-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="a95c3-116">Следующий скрипт анализирует значение строки даты и времени (DateTime) в предложении DECLARE.</span><span class="sxs-lookup"><span data-stu-id="a95c3-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="a95c3-117">Использование выражений C# для преобразования типов данных</span><span class="sxs-lookup"><span data-stu-id="a95c3-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="a95c3-118">В примере ниже описывается преобразование данных datetime с помощью выражений C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="a95c3-119">В этом конкретном случае строковые данные о дате и времени преобразуются в стандартное значение datetime использованием формата времени полуночи (00:00:00).</span><span class="sxs-lookup"><span data-stu-id="a95c3-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="a95c3-120">Использование выражений C# для получения текущей даты</span><span class="sxs-lookup"><span data-stu-id="a95c3-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="a95c3-121">Получить текущую дату можно с помощью следующего выражения C#:</span><span class="sxs-lookup"><span data-stu-id="a95c3-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="a95c3-122">Ниже приведен пример использования этого выражения в скрипте.</span><span class="sxs-lookup"><span data-stu-id="a95c3-122">Here's an example of how to use this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="a95c3-123">Использование сборок .NET</span><span class="sxs-lookup"><span data-stu-id="a95c3-123">Using .NET assemblies</span></span>
<span data-ttu-id="a95c3-124">Модель расширяемости U-SQL реализована как возможность добавлять пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="a95c3-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="a95c3-125">В настоящее время U-SQL предоставляет простые способы добавления собственного кода на базе Microsoft .NET (в частности, C#).</span><span class="sxs-lookup"><span data-stu-id="a95c3-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="a95c3-126">Однако вы также можете добавить пользовательский код, написанный на других языках .NET, например на VB.NET или F#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="a95c3-127">Регистрация сборки .NET</span><span class="sxs-lookup"><span data-stu-id="a95c3-127">Register a .NET assembly</span></span>

<span data-ttu-id="a95c3-128">Используйте инструкции CREATE ASSEMBLY, чтобы поместить сборку в базу данных U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="a95c3-129">Когда сборка попадает в базу данных, скрипты U-SQL могут использовать эти сборки с помощью инструкции REFERENCE ASSEMBLY.</span><span class="sxs-lookup"><span data-stu-id="a95c3-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="a95c3-130">Следующий код показывает, как зарегистрировать сборку:</span><span class="sxs-lookup"><span data-stu-id="a95c3-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="a95c3-131">Следующий код показывает, как сослаться на сборку:</span><span class="sxs-lookup"><span data-stu-id="a95c3-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="a95c3-132">Дополнительные сведения о регистрации сборки см. в [этой статье](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/).</span><span class="sxs-lookup"><span data-stu-id="a95c3-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="a95c3-133">Использование версий сборок</span><span class="sxs-lookup"><span data-stu-id="a95c3-133">Use assembly versioning</span></span>
<span data-ttu-id="a95c3-134">В настоящее время в U-SQL используется платформа .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="a95c3-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="a95c3-135">Убедитесь, что ваши сборки совместимы с этой версией среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="a95c3-136">Как упоминалось выше, U-SQL выполняет код в 64-разрядном формате (x64).</span><span class="sxs-lookup"><span data-stu-id="a95c3-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="a95c3-137">Поэтому код нужно компилировать так, чтобы он выполнялся в среде x64.</span><span class="sxs-lookup"><span data-stu-id="a95c3-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="a95c3-138">В противном случае вы получите ошибку неправильного формата, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="a95c3-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="a95c3-139">Любой передаваемый в хранилище файл (библиотеки DLL, файлы ресурсов, включая другие среды выполнения, машинные сборки, файлы конфигурации и т. д.) не может быть более 400 МБ.</span><span class="sxs-lookup"><span data-stu-id="a95c3-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="a95c3-140">Общий размер всех ресурсов, развернутых с помощью инструкции DEPLOY RESOURCE или с использованием ссылок на сборки и связанные файлы, не может превышать 3 ГБ.</span><span class="sxs-lookup"><span data-stu-id="a95c3-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="a95c3-141">И наконец, важно помнить, что в каждой базе данных U-SQL может быть только одна версия любой сборки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="a95c3-142">Например, если вам одновременно нужны версии 7 и 8 библиотеки NewtonSoft Json.Net, их следует зарегистрировать в разных базах данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="a95c3-143">Кроме того, каждый скрипт может ссылаться только на одну версию библиотеки DLL для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="a95c3-144">В этом отношении U-SQL соблюдает семантику C# управления сборками и версиями.</span><span class="sxs-lookup"><span data-stu-id="a95c3-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="a95c3-145">Использование определяемых пользователем функций</span><span class="sxs-lookup"><span data-stu-id="a95c3-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="a95c3-146">В языке U-SQL концепция определяемых пользователем функций обозначает подпрограммы, которые принимают параметры, выполняют действия (например, сложные вычисления) и возвращают результат этого действия в виде определенного значения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="a95c3-147">Определяемая пользователем функция может возвращать только одно скалярное значение.</span><span class="sxs-lookup"><span data-stu-id="a95c3-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="a95c3-148">Основной скрипт U-SQL может вызывать такие функции, как и любую другую скалярную функцию C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="a95c3-149">Мы советуем инициализировать определяемые пользователем функции U-SQL как **общедоступные** (public) и **статические** (static).</span><span class="sxs-lookup"><span data-stu-id="a95c3-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="a95c3-150">Сначала давайте рассмотрим простой пример создания определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="a95c3-151">В этом сценарии нужно определить финансовый период (квартал и месяц) для первого входа в систему определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="a95c3-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="a95c3-152">Финансовый год для этого примера начинается в июне.</span><span class="sxs-lookup"><span data-stu-id="a95c3-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="a95c3-153">Чтобы вычислить финансовый период, мы создаем следующую функцию C#:</span><span class="sxs-lookup"><span data-stu-id="a95c3-153">To calculate fiscal period, we introduce the following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="a95c3-154">Она вычисляет финансовый месяц и квартал и возвращает строковое значение.</span><span class="sxs-lookup"><span data-stu-id="a95c3-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="a95c3-155">Для июня (первый месяц первого финансового квартала) используются значения "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="a95c3-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="a95c3-156">Для июля — "Q1:P2" и т. д.</span><span class="sxs-lookup"><span data-stu-id="a95c3-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="a95c3-157">В нашем проекте U-SQL мы будем использовать базовые функции C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="a95c3-158">Вот как выглядит раздел кода программной части для этого примера:</span><span class="sxs-lookup"><span data-stu-id="a95c3-158">Here is how the code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="a95c3-159">Теперь мы вызовем эту функцию из основного скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="a95c3-160">Для этого нам нужно предоставить полное имя функции, включая пространство имен, в формате: "Пространство_имен.Класс.Функция(параметр)".</span><span class="sxs-lookup"><span data-stu-id="a95c3-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="a95c3-161">Так будет выглядеть вызов в основном скрипте U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a95c3-161">Following is the actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="a95c3-162">Ниже приведен файл выходных данных с результатом выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="a95c3-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="a95c3-163">Это простой пример использования встроенной определяемой пользователем функции в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="a95c3-164">Сохранение состояния между вызовами определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="a95c3-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="a95c3-165">Объекты, поддерживающие программирование C# в U-SQL, могут быть более сложными. Например, они могут интерактивно взаимодействовать через глобальные переменные кода программной части.</span><span class="sxs-lookup"><span data-stu-id="a95c3-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="a95c3-166">Рассмотрим приведенный ниже сценарий использования.</span><span class="sxs-lookup"><span data-stu-id="a95c3-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="a95c3-167">В больших организациях пользователи могут переключаться между разными внутренними приложениями,</span><span class="sxs-lookup"><span data-stu-id="a95c3-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="a95c3-168">включая Microsoft Dynamics CRM, Power BI и т. д.</span><span class="sxs-lookup"><span data-stu-id="a95c3-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="a95c3-169">Клиенты могут захотеть применить анализ телеметрии для пользовательских переключений между различными приложениями, например оценить тенденции использования и т. д.</span><span class="sxs-lookup"><span data-stu-id="a95c3-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="a95c3-170">Цель для бизнеса — оптимизация использования приложений.</span><span class="sxs-lookup"><span data-stu-id="a95c3-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="a95c3-171">Они могут также пожелать объединить различные приложения или процедуры входа.</span><span class="sxs-lookup"><span data-stu-id="a95c3-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="a95c3-172">Чтобы достичь этой цели, мы должны определить идентификаторы сеансов и интервалы задержки между последними сеансами.</span><span class="sxs-lookup"><span data-stu-id="a95c3-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="a95c3-173">Нам нужно найти предыдущий вход и привязать этот вход ко всем сеансам, создаваемым для одного и того же приложения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="a95c3-174">Первая трудность заключается в том, что основной скрипт U-SQL не позволяет производить вычисления с функцией LAG над уже вычисленным столбцом.</span><span class="sxs-lookup"><span data-stu-id="a95c3-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="a95c3-175">Вторая трудность — мы хотим сохранить определенный сеанс для всех сеансов за тот же интервал.</span><span class="sxs-lookup"><span data-stu-id="a95c3-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="a95c3-176">Чтобы решить эту проблему, мы используем глобальную переменную в разделе кода программной части `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="a95c3-177">Эта глобальная переменная применяется для всего набора строк во время выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="a95c3-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="a95c3-178">Так будет выглядеть раздел кода программной части для программы U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a95c3-178">Here is the code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="a95c3-179">Как видно из этого примера, глобальная переменная `static public string globalSession;` используется внутри функции `getStampUserSession` и инициализируется заново каждый раз, когда изменяется значение параметра сеанса.</span><span class="sxs-lookup"><span data-stu-id="a95c3-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="a95c3-180">Основной скрипт U-SQL выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a95c3-180">The U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="a95c3-181">Функция `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` вызывается здесь во время вычисления второго набора строк в памяти.</span><span class="sxs-lookup"><span data-stu-id="a95c3-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="a95c3-182">Она передает столбец `UserSessionTimestamp` и возвращает значение до изменения `UserSessionTimestamp`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="a95c3-183">Выходной файл будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a95c3-183">The output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="a95c3-184">В этом примере мы видим более сложный сценарий использования, в котором глобальная переменная используется в разделе кода программной части для всего набора строк в памяти.</span><span class="sxs-lookup"><span data-stu-id="a95c3-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="a95c3-185">Использование определяемых пользователем типов данных</span><span class="sxs-lookup"><span data-stu-id="a95c3-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="a95c3-186">Определяемые пользователем типы или UDT — это еще одно средство, поддерживающее возможность программирования в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="a95c3-187">Определяемый пользователем тип в U-SQL действует так же, как аналогичный тип в C#.</span><span class="sxs-lookup"><span data-stu-id="a95c3-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="a95c3-188">C# — это строго типизированный язык, в котором можно использовать встроенные и пользовательские типы данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="a95c3-189">U-SQL не может неявно сериализировать или десериализировать произвольные пользовательские типы данных, когда пользовательский тип данных передается между вершинами в наборах строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="a95c3-190">Поэтому пользователь должен указать явный модуль форматирования с помощью интерфейса IFormatter.</span><span class="sxs-lookup"><span data-stu-id="a95c3-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="a95c3-191">Таким образом, U-SQL получит методы сериализации и десериализации для пользовательских типов данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="a95c3-192">Встроенные средства извлечения и вывода U-SQL в настоящее время не могут сериализировать или десериализировать пользовательские типы данных в файлы или из них, даже если они используют набор IFormatter.</span><span class="sxs-lookup"><span data-stu-id="a95c3-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="a95c3-193">Поэтому, если вы записываете пользовательские типы данных в файл с помощью инструкции OUTPUT или считываете их с помощью средств извлечения, вам необходимо передать их в качестве массива строк или байтов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="a95c3-194">Затем необходимо явным образом вызвать код сериализации и десериализации (метод пользовательских типов данных ToString()).</span><span class="sxs-lookup"><span data-stu-id="a95c3-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="a95c3-195">Но пользовательские средства извлечения и вывода могут читать и записывать пользовательские типы данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="a95c3-196">При попытке использования пользовательского типа в средствах EXTRACTOR и OUTPUTTER (на основе инструкции SELECT), как показано ниже,</span><span class="sxs-lookup"><span data-stu-id="a95c3-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="a95c3-197">мы получим такую ошибку:</span><span class="sxs-lookup"><span data-stu-id="a95c3-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="a95c3-198">Для работы с определяемым пользователем типом в средстве OUTPUTTER мы должны сериализовать данные в строку с помощью метода ToString() или создать пользовательское средство OUTPUTTER.</span><span class="sxs-lookup"><span data-stu-id="a95c3-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="a95c3-199">Сейчас определяемые пользователем типы нельзя использовать в инструкции GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="a95c3-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="a95c3-200">Если определяемый пользователем тип будет использован в GROUP BY, возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a95c3-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="a95c3-201">Чтобы определить пользовательский тип, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a95c3-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="a95c3-202">Добавьте приведенные ниже пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a95c3-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="a95c3-203">Добавьте `Microsoft.Analytics.Interfaces` для интерфейсов определяемых пользователем типов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="a95c3-204">Кроме того, `System.IO` может потребоваться для определения интерфейса IFormatter.</span><span class="sxs-lookup"><span data-stu-id="a95c3-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="a95c3-205">Определите определяемый пользователем тип данных с помощью атрибута SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="a95c3-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="a95c3-206">**SqlUserDefinedType** указывает, что определение типа в сборке представляет определяемый пользователем тип данных для U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="a95c3-207">Свойства этого атрибута отражают физические характеристики определяемого пользователем типа данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="a95c3-208">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-208">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-209">SqlUserDefinedType является обязательным атрибутом для определяемых пользователем типов данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="a95c3-210">Ниже представлен конструктор для этого класса.</span><span class="sxs-lookup"><span data-stu-id="a95c3-210">The constructor of the class:</span></span>  

* <span data-ttu-id="a95c3-211">SqlUserDefinedTypeAttribute (модуль форматирования).</span><span class="sxs-lookup"><span data-stu-id="a95c3-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="a95c3-212">Модуль форматирования — обязательный параметр, определяющий форматирование для определяемого пользователем типа данных. Здесь нужно передать тип интерфейса `IFormatter`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="a95c3-213">Типичные определяемые пользователем типы данных также требуют определения интерфейса IFormatter, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="a95c3-214">Интерфейс `IFormatter` — для сериализации и десериализации графа объекта с корневым типом \<typeparamref name="T">.</span><span class="sxs-lookup"><span data-stu-id="a95c3-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="a95c3-215">\<typeparam name="T"> Это корневой тип графа объекта для сериализации и десериализации.</span><span class="sxs-lookup"><span data-stu-id="a95c3-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="a95c3-216">**Десериализация** — процесс, обратный сериализации данных в предоставленном потоке, в ходе которого воспроизводится граф объектов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="a95c3-217">**Сериализация** — процесс сериализации объекта или графа объектов с использованием заданного корня в предоставленный поток.</span><span class="sxs-lookup"><span data-stu-id="a95c3-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="a95c3-218">Экземпляр `MyType` — экземпляр типа.</span><span class="sxs-lookup"><span data-stu-id="a95c3-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="a95c3-219">Модуль записи `IColumnWriter` или чтения `IColumnReader` — базовый поток столбца.</span><span class="sxs-lookup"><span data-stu-id="a95c3-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="a95c3-220">Контекст `ISerializationContext` — перечисление, которое определяет набор флагов, указывающих контекст источника или назначения для потока во время сериализации.</span><span class="sxs-lookup"><span data-stu-id="a95c3-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="a95c3-221">**Intermediate** — указывает, что исходный или целевой контекст не является материализованным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="a95c3-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="a95c3-222">**Persistent** — указывает, что исходный или целевой контекст является материализованным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="a95c3-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="a95c3-223">Как и обычный тип C#, определение определяемого пользователем типа данных в U-SQL может переопределять такие операторы, как +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="a95c3-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="a95c3-224">Также оно может содержать статические методы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-224">It can also include static methods.</span></span> <span data-ttu-id="a95c3-225">Например, если мы собираемся использовать этот определяемый пользователем тип данных в качестве параметра агрегатной функции MIN U-SQL, нужно переопределить оператор <.</span><span class="sxs-lookup"><span data-stu-id="a95c3-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="a95c3-226">Ранее в этой статье мы привели пример, в котором определяли финансовый период для конкретной даты в формате Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="a95c3-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="a95c3-227">Следующий пример показывает, как использовать определяемый пользователем тип данных для значений финансового периода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="a95c3-228">Ниже приведен пример раздела кода программной части с определяемым пользователем типом данных и интерфейсом IFormatter.</span><span class="sxs-lookup"><span data-stu-id="a95c3-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="a95c3-229">Определяемый тип содержит два числа: квартал и месяц.</span><span class="sxs-lookup"><span data-stu-id="a95c3-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="a95c3-230">Здесь определены операторы ==, ! =, >, < и статический метод ToString().</span><span class="sxs-lookup"><span data-stu-id="a95c3-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="a95c3-231">Как упоминалось выше, определяемый пользователем тип данных можно использовать в выражениях SELECT, но нельзя — в средствах OUTPUTTER и EXTRACTOR без настраиваемой сериализации.</span><span class="sxs-lookup"><span data-stu-id="a95c3-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="a95c3-232">Нужно сериализовать его в строку с помощью метода ToString() или использовать пользовательское средство OUTPUTTER или EXTRACTOR.</span><span class="sxs-lookup"><span data-stu-id="a95c3-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="a95c3-233">Теперь давайте рассмотрим, как можно применять определяемый пользователем тип данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="a95c3-234">В разделе кода программной части мы изменили функцию GetFiscalPeriod следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a95c3-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="a95c3-235">Как видите, он возвращает значение с типом данных FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="a95c3-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="a95c3-236">Ниже приведен пример его дальнейшего использования в основном скрипте U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="a95c3-237">В этом примере представлено несколько способов вызова определяемого пользователем типа данных из скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="a95c3-238">Ниже приведен пример полного раздела кода программной части.</span><span class="sxs-lookup"><span data-stu-id="a95c3-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="a95c3-239">Использование определяемых пользователем статистических функций</span><span class="sxs-lookup"><span data-stu-id="a95c3-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="a95c3-240">Определяемые пользователем статистические выражения — это любые функции статистической обработки, не входящие в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="a95c3-241">Например, это может быть статистическое выражение для пользовательских математических вычислений, объединения строк, манипуляций с ними и т. д.</span><span class="sxs-lookup"><span data-stu-id="a95c3-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="a95c3-242">Определение базового класса определяемого пользователем статистического выражения представлено ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-242">The user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="a95c3-243">**SqlUserDefinedAggregate** указывает, что тип должен быть зарегистрирован как определяемая пользователем статистическая функция.</span><span class="sxs-lookup"><span data-stu-id="a95c3-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="a95c3-244">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-244">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-245">Атрибут SqlUserDefinedType является **необязательным** для определяемого пользователем статистического выражения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="a95c3-246">Базовый класс позволяет передать три абстрактных параметра — два входных и один в качестве результата.</span><span class="sxs-lookup"><span data-stu-id="a95c3-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="a95c3-247">Типы данных представлены переменными, которые должны быть определены при наследовании классов:</span><span class="sxs-lookup"><span data-stu-id="a95c3-247">The data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="a95c3-248">**Init** — метод, который вызывается один раз для каждой группы во время вычисления.</span><span class="sxs-lookup"><span data-stu-id="a95c3-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="a95c3-249">Он предоставляет процедуры инициализации для каждой группы статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="a95c3-250">**Accumulate** — метод, который выполняется один раз для каждого значения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="a95c3-251">Он выполняет основную работу алгоритма статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="a95c3-252">Его можно использовать для обработки значений с разными типами данных, определяемыми при наследовании класса.</span><span class="sxs-lookup"><span data-stu-id="a95c3-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="a95c3-253">Он может принимать два параметра разных типов данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="a95c3-254">**Terminate** — метод, который выполняется один раз на каждую группу статистической обработки в конце обработки, чтобы вывести результаты по каждой группе.</span><span class="sxs-lookup"><span data-stu-id="a95c3-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="a95c3-255">Чтобы объявить правильные типы входных и выходных данных, используйте определение класса, приведенное ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="a95c3-256">T1 — первый параметр для метода Accumulate.</span><span class="sxs-lookup"><span data-stu-id="a95c3-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="a95c3-257">T2 — второй параметр для метода Accumulate.</span><span class="sxs-lookup"><span data-stu-id="a95c3-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="a95c3-258">TResult — возвращаемый тип для метода Terminate.</span><span class="sxs-lookup"><span data-stu-id="a95c3-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="a95c3-259">Например:</span><span class="sxs-lookup"><span data-stu-id="a95c3-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="a95c3-260">или</span><span class="sxs-lookup"><span data-stu-id="a95c3-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="a95c3-261">Использование определяемых пользователем статистических выражений в U-SQL</span><span class="sxs-lookup"><span data-stu-id="a95c3-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="a95c3-262">Чтобы применить определяемое пользователем статистическое выражение, сначала определите его в коде программной части или укажите на него ссылку из существующих библиотек DLL для программирования, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a95c3-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="a95c3-263">Затем используйте приведенный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="a95c3-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="a95c3-264">Ниже приведен пример определяемого пользователем статистического выражения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="a95c3-265">И основной скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="a95c3-266">В этом сценарии мы объединяем значения идентификаторов класса для определенных пользователей.</span><span class="sxs-lookup"><span data-stu-id="a95c3-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="a95c3-267">Использование определяемых пользователем объектов</span><span class="sxs-lookup"><span data-stu-id="a95c3-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="a95c3-268">U-SQL предоставляет возможность определять пользовательские объекты, поддерживающие программирование, которые называют определяемыми пользователями объектами.</span><span class="sxs-lookup"><span data-stu-id="a95c3-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="a95c3-269">Ниже приведен список определяемых пользователем объектов в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="a95c3-270">Пользовательские средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-270">User-defined extractors</span></span>
    * <span data-ttu-id="a95c3-271">Извлечение по строкам.</span><span class="sxs-lookup"><span data-stu-id="a95c3-271">Extract row by row</span></span>
    * <span data-ttu-id="a95c3-272">Используется для реализации извлечения данных из пользовательских структурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="a95c3-273">Пользовательские средства вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-273">User-defined outputters</span></span>
    * <span data-ttu-id="a95c3-274">Вывод по строкам.</span><span class="sxs-lookup"><span data-stu-id="a95c3-274">Output row by row</span></span>
    * <span data-ttu-id="a95c3-275">Используется для вывода пользовательских типов данных или пользовательских форматов файлов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="a95c3-276">Пользовательские средства обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-276">User-defined processors</span></span>
    * <span data-ttu-id="a95c3-277">Получение одной строки и возврат одной строки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="a95c3-278">Используется для сокращения числа столбцов или создания новых столбцов, значения которых основаны на значениях существующего набора столбцов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="a95c3-279">Пользовательские средства применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-279">User-defined appliers</span></span>
    * <span data-ttu-id="a95c3-280">Получение одной строки и возврат от 0 до n строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="a95c3-281">Использование с инструкциями OUTER и CROSS APPLY.</span><span class="sxs-lookup"><span data-stu-id="a95c3-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="a95c3-282">Пользовательские средства объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-282">User-defined combiners</span></span>
    * <span data-ttu-id="a95c3-283">Объединяют наборы строк — определяемые пользователем инструкции JOIN.</span><span class="sxs-lookup"><span data-stu-id="a95c3-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="a95c3-284">Пользовательские средства редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-284">User-defined reducers</span></span>
    * <span data-ttu-id="a95c3-285">Получение n строк и возврат одной строки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="a95c3-286">Используется для сокращения числа строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="a95c3-287">Обычно определяемые пользователем объекты вызываются явным образом в скрипте U-SQL при выполнении следующих инструкций U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a95c3-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="a95c3-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="a95c3-288">EXTRACT</span></span>
* <span data-ttu-id="a95c3-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="a95c3-289">OUTPUT</span></span>
* <span data-ttu-id="a95c3-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="a95c3-290">PROCESS</span></span>
* <span data-ttu-id="a95c3-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="a95c3-291">COMBINE</span></span>
* <span data-ttu-id="a95c3-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="a95c3-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="a95c3-293">Определяемые пользователем объекты ограничены потреблением 0,5 ГБ памяти.</span><span class="sxs-lookup"><span data-stu-id="a95c3-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="a95c3-294">Это ограничение памяти не применяется для локальных выполнений.</span><span class="sxs-lookup"><span data-stu-id="a95c3-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="a95c3-295">Использование пользовательских средств извлечения</span><span class="sxs-lookup"><span data-stu-id="a95c3-295">Use user-defined extractors</span></span>
<span data-ttu-id="a95c3-296">U-SQL позволяет импортировать внешние данные с помощью инструкции EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="a95c3-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="a95c3-297">Инструкция EXTRACT может использовать встроенные средства извлечения для определяемых пользователем объектов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="a95c3-298">*Extractors.Text()*: извлекает данные из текстовых файлов с разделителями в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="a95c3-299">*Extractors.Csv()*: извлекает данные из файлов данных с разделителями-запятыми (CSV) в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="a95c3-300">*Extractors.Csv()*: извлекает данные из файлов со значением с разделением знаками табуляции (TSV), в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="a95c3-301">Можно также разработать пользовательское средство извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="a95c3-302">Например, если при импорте данных нам нужно выполнить одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="a95c3-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="a95c3-303">Изменить входные данные, разделяя столбцы или изменяя отдельные значения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="a95c3-304">Для объединения строк лучше всего использовать PROCESSOR.</span><span class="sxs-lookup"><span data-stu-id="a95c3-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="a95c3-305">Выполнить синтаксический анализ неструктурированных данных, например веб-страниц или сообщений электронной почты, или частично структурированных данных, например документов XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="a95c3-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="a95c3-306">Выполнить анализ данных в неподдерживаемых кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="a95c3-307">Чтобы определить пользовательское средство извлечения, нужно создать интерфейс `IExtractor`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="a95c3-308">Все входные параметры средства извлечения, такие как разделители столбцов и строк, кодировки, должны быть определены в конструкторе класса.</span><span class="sxs-lookup"><span data-stu-id="a95c3-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="a95c3-309">Интерфейс `IExtractor` также должен содержать определение для переопределения `IEnumerable<IRow>`:</span><span class="sxs-lookup"><span data-stu-id="a95c3-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="a95c3-310">Атрибут **SqlUserDefinedExtractor** указывает, что этот тип должен быть зарегистрирован как пользовательское средство извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="a95c3-311">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-311">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-312">SqlUserDefinedExtractor — это необязательный атрибут для определения пользовательского средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="a95c3-313">Он используется для определения свойства AtomicFileProcessing:</span><span class="sxs-lookup"><span data-stu-id="a95c3-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="a95c3-314">bool AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="a95c3-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="a95c3-315">Значение **true** указывает, что это средство извлечения требует атомарные входные файлы (JSON, XML и другие).</span><span class="sxs-lookup"><span data-stu-id="a95c3-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="a95c3-316">Значение **false** указывает, что это средство извлечения умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).</span><span class="sxs-lookup"><span data-stu-id="a95c3-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="a95c3-317">Основные объекты в пользовательских объектах, поддерживающих программирование, — это **input** (ввод) и **output** (вывод).</span><span class="sxs-lookup"><span data-stu-id="a95c3-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="a95c3-318">Объект input используется для перечисления входных данных как `IUnstructuredReader`,</span><span class="sxs-lookup"><span data-stu-id="a95c3-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="a95c3-319">объект output — для вывода данных, полученных в результате действий по извлечению.</span><span class="sxs-lookup"><span data-stu-id="a95c3-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="a95c3-320">Получить доступ к входным данным можно через `System.IO.Stream` и `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="a95c3-321">Чтобы перечислить входные столбцы, необходимо сначала разбить входной поток, используя разделитель строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="a95c3-322">Затем еще раз разбиваем входную строку на столбцы:</span><span class="sxs-lookup"><span data-stu-id="a95c3-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="a95c3-323">Чтобы сохранить выходные данные, мы используем метод `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="a95c3-324">Необходимо понимать, что пользовательское средство извлечения только выводит столбцы и значения, определяемые выходными данными.</span><span class="sxs-lookup"><span data-stu-id="a95c3-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="a95c3-325">Вызов метода Set:</span><span class="sxs-lookup"><span data-stu-id="a95c3-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="a95c3-326">Фактический вывод данных из средства извлечения инициируется вызовом метода `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="a95c3-327">Ниже приведен пример средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-327">Following is the extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="a95c3-328">В этом сценарии средство извлечения восстанавливает идентификатор для столбца guid и преобразует значения столбца user в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="a95c3-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="a95c3-329">Пользовательские средства извлечения могут создавать более сложные результаты, анализируя входные данные и преобразовывая их.</span><span class="sxs-lookup"><span data-stu-id="a95c3-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="a95c3-330">Ниже представлен основной скрипт U-SQL, который использует пользовательское средство извлечения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="a95c3-331">Использование пользовательских средств вывода</span><span class="sxs-lookup"><span data-stu-id="a95c3-331">Use user-defined outputters</span></span>
<span data-ttu-id="a95c3-332">Пользовательское средство вывода — это еще один определяемый пользователем объект U-SQL, который позволяет расширить встроенные возможности U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="a95c3-333">Как и средства извлечения, существует несколько встроенных средств вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="a95c3-334">*Outputters.Text()*: записывает данные в текстовые файлы с разделителями в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="a95c3-335">*Outputters.Csv()*: записывает данные в файлы с разделителями-запятыми (CSV) в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="a95c3-336">*Outputters.Tsv()*: записывает данные в файлы со значениями с разделением знаками табуляции (TSV) в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="a95c3-337">Пользовательские средства вывода позволяют записывать данные в определяемом пользователем формате.</span><span class="sxs-lookup"><span data-stu-id="a95c3-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="a95c3-338">Это может потребоваться для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="a95c3-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="a95c3-339">Запись данных в частично структурированные или неструктурированные файлы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="a95c3-340">Запись данных в неподдерживаемых кодировках.</span><span class="sxs-lookup"><span data-stu-id="a95c3-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="a95c3-341">Преобразование выходных данных или добавление пользовательских атрибутов.</span><span class="sxs-lookup"><span data-stu-id="a95c3-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="a95c3-342">Чтобы определить пользовательское средство вывода, нужно создать интерфейс `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="a95c3-343">Ниже приведена базовая реализация класса `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="a95c3-344">Все входные параметры средства вывода, такие как разделители столбцов и строк, кодировки и т. д., должны быть определены в конструкторе класса.</span><span class="sxs-lookup"><span data-stu-id="a95c3-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="a95c3-345">Интерфейс `IOutputter` также должен содержать определение для переопределения `void Output`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="a95c3-346">При необходимости для атомарной обработки файлов можно задать атрибут `[SqlUserDefinedOutputter(AtomicFileProcessing = true)`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="a95c3-347">Дополнительные сведения см. ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-347">For more information, see the following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="a95c3-348">Метод `Output` вызывается для каждой входной строки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-348">`Output` is called for each input row.</span></span> <span data-ttu-id="a95c3-349">Он возвращает набор строк `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="a95c3-350">Класс Constructor используется для передачи параметров в пользовательское средство вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="a95c3-351">Метод `Close` при необходимости можно переопределить, чтобы выходить из ресурсозатратных состояний или узнавать время записи последней строки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="a95c3-352">Атрибут **SqlUserDefinedAggregate** указывает, что этот тип должен быть зарегистрирован как пользовательское средство вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="a95c3-353">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-353">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-354">SqlUserDefinedOutputter — это необязательный атрибут для определения пользовательских средств вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="a95c3-355">Он используется для определения свойства AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="a95c3-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="a95c3-356">bool AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="a95c3-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="a95c3-357">**true** — указывает, что это средство вывода требует атомарные выходные файлы (JSON, XML и другие).</span><span class="sxs-lookup"><span data-stu-id="a95c3-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="a95c3-358">**false** — указывает, что это средство вывода умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).</span><span class="sxs-lookup"><span data-stu-id="a95c3-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="a95c3-359">Основные объекты, поддерживающие программирование, — это **row** (строка) и **output** (вывод).</span><span class="sxs-lookup"><span data-stu-id="a95c3-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="a95c3-360">Объект **row** используется для перечисления выходных данных в интерфейсе `IRow`,</span><span class="sxs-lookup"><span data-stu-id="a95c3-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="a95c3-361">а объект **output** — для отправки выходных данных в конечный файл.</span><span class="sxs-lookup"><span data-stu-id="a95c3-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="a95c3-362">Обращение к выходным данным выполняется через интерфейс `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="a95c3-363">Выходные данные передаются построчно.</span><span class="sxs-lookup"><span data-stu-id="a95c3-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="a95c3-364">Отдельные значения перечисляются с помощью вызова метода Get интерфейса IRow.</span><span class="sxs-lookup"><span data-stu-id="a95c3-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="a95c3-365">Имена отдельных столбцов можно определить с помощью вызова метода `row.Schema`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="a95c3-366">Такой подход позволяет создавать гибкие средства вывода для любой схемы метаданных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="a95c3-367">Выходные данные записываются в файл с помощью `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="a95c3-368">Для параметра потока задано значение `output.BaseStrea` в структуре `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="a95c3-369">Обратите внимание, что после каждой итерации строк необходимо очищать буфер данных для файла.</span><span class="sxs-lookup"><span data-stu-id="a95c3-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="a95c3-370">Кроме того, объект `StreamWriter` должен использоваться с включенным (по умолчанию) атрибутом Disposable и с ключевым словом **using**.</span><span class="sxs-lookup"><span data-stu-id="a95c3-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="a95c3-371">В противном случае — после каждой итерации вызывайте явным образом метод Flush().</span><span class="sxs-lookup"><span data-stu-id="a95c3-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="a95c3-372">Это описано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="a95c3-373">Установка колонтитулов для пользовательского средства вывода</span><span class="sxs-lookup"><span data-stu-id="a95c3-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="a95c3-374">Чтобы задать верхний колонтитул, используйте последовательность однократного выполнения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-374">To set a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="a95c3-375">Код в первом блоке `if (isHeaderRow)` выполняется только один раз.</span><span class="sxs-lookup"><span data-stu-id="a95c3-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="a95c3-376">Для нижнего колонтитула используйте ссылку на экземпляр `System.IO.Stream` объекта `output.BaseStream`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="a95c3-377">Запишите нижний колонтитул в метод Close() интерфейса `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="a95c3-378">(Дополнительные сведения см. ниже.)</span><span class="sxs-lookup"><span data-stu-id="a95c3-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="a95c3-379">Ниже приведен пример пользовательского средства вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="a95c3-380">И основной скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="a95c3-381">Это средство вывода для формата HTML. Оно создает HTML-файл с данными таблицы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="a95c3-382">Вызов средства вывода из основного скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="a95c3-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="a95c3-383">Чтобы вызвать пользовательское средство вывода из основного скрипта U-SQL, нужно создать новый экземпляр объекта для средства вывода.</span><span class="sxs-lookup"><span data-stu-id="a95c3-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="a95c3-384">Чтобы не создавать экземпляр объекта в основном скрипте, мы можем создать оболочку функции, как было показано в примере выше.</span><span class="sxs-lookup"><span data-stu-id="a95c3-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="a95c3-385">В этом случае исходный вызов будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a95c3-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="a95c3-386">Использование пользовательских средств обработки</span><span class="sxs-lookup"><span data-stu-id="a95c3-386">Use user-defined processors</span></span>
<span data-ttu-id="a95c3-387">Пользовательское средство обработки — это тип определяемого пользователем объекта U-SQL, который позволяет обрабатывать входящие строки, применяя к ним средства программирования.</span><span class="sxs-lookup"><span data-stu-id="a95c3-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="a95c3-388">Оно позволяет объединять столбцы, изменять значения или добавлять новые столбцы при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a95c3-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="a95c3-389">По сути оно позволяет получить нужные элементы данных, обрабатывая наборы строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="a95c3-390">Чтобы определить пользовательское средство обработки, нужно создать интерфейс `IProcessor` с атрибутом `SqlUserDefinedProcessor`, который является необязательным для этого средства.</span><span class="sxs-lookup"><span data-stu-id="a95c3-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="a95c3-391">Этот интерфейс должен содержать определение для переопределения набора строк интерфейса `IRow`, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="a95c3-392">**SqlUserDefinedProcessor** указывает, что тип должен быть зарегистрирован как пользовательское средство обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="a95c3-393">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-393">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-394">Атрибут SqlUserDefinedProcessor является **необязательным** для определения пользовательского средства обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="a95c3-395">Основные объекты, поддерживающие программирование, — это **input** (ввод) и **output** (вывод).</span><span class="sxs-lookup"><span data-stu-id="a95c3-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="a95c3-396">Объект input используется для перечисления входных столбцов, а объект output — для вывода данных, полученных в результате действий по обработке.</span><span class="sxs-lookup"><span data-stu-id="a95c3-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="a95c3-397">Для перечисления входных столбцов мы используем метод `input.Get`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="a95c3-398">Параметр для метода `input.Get` — это столбец, представленный в предложении `PRODUCE` для инструкции `PROCESS` в основном скрипте U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="a95c3-399">Здесь необходимо использовать правильный тип данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="a95c3-400">Для выходных данных используйте метод `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="a95c3-401">Необходимо понимать, что пользовательское средство только выводит столбцы и значения, определяемые вызовом метода `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="a95c3-402">Фактический вывод данных из средства обработки инициируется вызовом метода `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="a95c3-403">Ниже приведен пример использования средства обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="a95c3-404">В этом сценарии использования средство обработки создает новый столбец с именем full_description путем объединения существующих столбцов — user в верхнем регистре и des.</span><span class="sxs-lookup"><span data-stu-id="a95c3-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="a95c3-405">Также оно заново создает идентификатор GUID и возвращает его исходное и новое значения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="a95c3-406">Как видно из примера выше, вы можете вызывать метод C# во время вызова метода `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="a95c3-407">Ниже приведен пример основного скрипта U-SQL, использующего пользовательское средство обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="a95c3-408">Использование пользовательских средств применения</span><span class="sxs-lookup"><span data-stu-id="a95c3-408">Use user-defined appliers</span></span>
<span data-ttu-id="a95c3-409">Пользовательское средство применения U-SQL позволяет вызывать пользовательскую функцию C# для каждой строки, возвращаемой выражением запроса к внешней таблице.</span><span class="sxs-lookup"><span data-stu-id="a95c3-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="a95c3-410">Входные данные справа оцениваются для каждой строки из входных данных слева, а затем созданные строки объединяются для итоговых выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="a95c3-411">Список столбцов, созданных оператором APPLY, — это сочетание набора столбцов из входных данных слева и справа.</span><span class="sxs-lookup"><span data-stu-id="a95c3-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="a95c3-412">Пользовательские средства применения вызываются как часть выражения USQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="a95c3-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="a95c3-413">Типичный вызов пользовательских средств применения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a95c3-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="a95c3-414">Дополнительные сведения об использовании средств применения в выражении SELECT см. в статье [U-SQL SELECT, выбрав из CROSS APPLY и OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="a95c3-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="a95c3-415">Ниже представлено определение базового класса пользовательского средства применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="a95c3-416">Чтобы определить пользовательское средство применения, нам необходимо создать интерфейс `IApplier` с атрибутом [`SqlUserDefinedApplier`], который не является обязательным для определения пользовательских средств применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="a95c3-417">Операция применения вызывается для каждой строки внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="a95c3-418">Она возвращает выходной набор строк `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="a95c3-419">Класс Constructor используется для передачи параметров в пользовательское средство применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="a95c3-420">**SqlUserDefinedApplier** указывает, что тип должен быть зарегистрирован как пользовательское средство применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="a95c3-421">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-421">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-422">Атрибут **SqlUserDefinedApplier** является **необязательным** для определения пользовательского средства применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="a95c3-423">Ниже представлены основные объекты, поддерживающие программирование.</span><span class="sxs-lookup"><span data-stu-id="a95c3-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="a95c3-424">Входной набор строк передается в виде ввода `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="a95c3-425">Выходные строки создаются как интерфейс вывода `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="a95c3-426">Имена отдельных столбцов можно узнать, вызвав метод схемы `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="a95c3-427">Чтобы получить фактические значения данных из входящего метода `IRow`, мы используем метод Get() интерфейса `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="a95c3-428">Или мы можем использовать имя столбца схемы:</span><span class="sxs-lookup"><span data-stu-id="a95c3-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="a95c3-429">Выходные значения следует передавать в выход `IUpdatableRow`:</span><span class="sxs-lookup"><span data-stu-id="a95c3-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="a95c3-430">Важно понимать, что пользовательские средства применения только выводят столбцы и значения, определенные вызовом метода `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="a95c3-431">Фактический вывод данных из средства применения инициируется вызовом метода `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="a95c3-432">Параметры пользовательских средств применения можно передать в конструктор.</span><span class="sxs-lookup"><span data-stu-id="a95c3-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="a95c3-433">Средство применения может возвращать переменное число столбцов, которое должно быть определено при вызове средства применения из основного скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="a95c3-434">Ниже приведен пример использования пользовательского средства применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-434">Here is the user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="a95c3-435">И основной скрипт U-SQL для этого пользовательского средства применения:</span><span class="sxs-lookup"><span data-stu-id="a95c3-435">Following is the base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="a95c3-436">В этом сценарии пользовательское средство применения действует как анализатор значений с разделителями-запятыми для набора свойств автомобильного парка.</span><span class="sxs-lookup"><span data-stu-id="a95c3-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="a95c3-437">Строки входного файла будут выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a95c3-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="a95c3-438">Это стандартный TSV-файл со значениями с разделением знаками табуляции, в котором столбец свойств содержит такие свойства автомобилей, как производитель, модель и т. д.</span><span class="sxs-lookup"><span data-stu-id="a95c3-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="a95c3-439">Эти свойства нужно проанализировать и преобразовать в столбцы таблицы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="a95c3-440">Предоставленное средство применения также позволяет создать динамическое число свойств в результирующем наборе строк на основе переданных параметров.</span><span class="sxs-lookup"><span data-stu-id="a95c3-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="a95c3-441">Вы можете создать либо все свойства, либо определенный набор свойств.</span><span class="sxs-lookup"><span data-stu-id="a95c3-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="a95c3-442">Пользовательское средство применения может вызываться как новый экземпляр средства применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="a95c3-443">Или с вызовом метода фабрики оболочки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="a95c3-444">Использование пользовательских средств объединения</span><span class="sxs-lookup"><span data-stu-id="a95c3-444">Use user-defined combiners</span></span>
<span data-ttu-id="a95c3-445">Пользовательское средство объединения позволяет объединить строки из левого и правого наборов строк, используя настраиваемую логику объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="a95c3-446">Пользовательское средство объединения используется с выражением COMBINE.</span><span class="sxs-lookup"><span data-stu-id="a95c3-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="a95c3-447">Средство объединения вызывается из выражения COMBINE, которое предоставляет необходимые сведения о входных наборах строк, столбцах для группирования, схеме ожидаемого результата, а также дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="a95c3-448">Чтобы вызвать средство объединения из основного скрипта U-SQL, используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="a95c3-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="a95c3-449">Дополнительные сведения см. в [описании выражения COMBINE для U-SQL](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="a95c3-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="a95c3-450">Чтобы задать пользовательское средство объединения, нам необходимо создать интерфейс `ICombiner` с атрибутом [`SqlUserDefinedCombiner`], который не является обязательным для определения пользовательских средств объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="a95c3-451">Определение базового класса `ICombiner`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="a95c3-452">Пользовательская реализация интерфейса `ICombiner` должна содержать определение для переопределения метода `IEnumerable<IRow>` Combine.</span><span class="sxs-lookup"><span data-stu-id="a95c3-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="a95c3-453">Атрибут **SqlUserDefinedCombiner** указывает, что этот тип должен быть зарегистрирован как пользовательское средство объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="a95c3-454">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-454">This class cannot be inherited.</span></span>

<span data-ttu-id="a95c3-455">Метод **SqlUserDefinedCombiner** используется для определения свойства режима объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="a95c3-456">Он является необязательным атрибутом для определения пользовательских средств объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="a95c3-457">Режимы CombinerMode</span><span class="sxs-lookup"><span data-stu-id="a95c3-457">CombinerMode     Mode</span></span>

<span data-ttu-id="a95c3-458">Перечисление CombinerMode может принимать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a95c3-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="a95c3-459">Full (0). Каждая строка выходных данных может зависеть от всех входных строк слева и справа с одинаковым значением ключа.</span><span class="sxs-lookup"><span data-stu-id="a95c3-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="a95c3-460">Left (1). Каждая строка выходных данных зависит от одной входной строки из левого входа (и потенциально от всех строк из правого входа с тем же значением ключа).</span><span class="sxs-lookup"><span data-stu-id="a95c3-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="a95c3-461">Right (2) — каждая строка выходных данных зависит от одной входной строки из правого входа (и потенциально от всех строк из левого входа с тем же значением ключа).</span><span class="sxs-lookup"><span data-stu-id="a95c3-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="a95c3-462">Inner (3). Каждая строка выходных данных зависит от одной строки из левого входа и одной строки из правого входа с тем же значением ключа.</span><span class="sxs-lookup"><span data-stu-id="a95c3-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="a95c3-463">Пример: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="a95c3-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="a95c3-464">Ниже представлены основные объекты, поддерживающие программирование.</span><span class="sxs-lookup"><span data-stu-id="a95c3-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="a95c3-465">Входные наборы строк передаются в виде левого (**left**) и правого (**right**) интерфейсов типа `IRowset`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="a95c3-466">Они должны быть перечислены для обработки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="a95c3-467">Каждый интерфейс можно перечислить только один раз, поэтому для повторной обработки их нужно перечислять с использованием кэша.</span><span class="sxs-lookup"><span data-stu-id="a95c3-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="a95c3-468">Для целей кэширования мы можем создать тип структуры памяти List\<T\> как результат выполнения запроса LINQ, в частности создать тип List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="a95c3-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="a95c3-469">Также для перечисления можно использовать анонимные типы данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="a95c3-470">Дополнительные сведения о запросах LINQ см. в статье [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) (Введение в запросы LINQ (C#)), а описание интерфейса IEnumerable\<T\> — в статье [Интерфейс IEnumerable\<T\>](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="a95c3-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="a95c3-471">Чтобы получить фактические значения данных из входящего метода `IRowset`, мы используем метод Get() интерфейса `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="a95c3-472">Имена отдельных столбцов можно узнать, вызвав метод схемы `IRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="a95c3-473">Или мы можем использовать имя столбца схемы:</span><span class="sxs-lookup"><span data-stu-id="a95c3-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="a95c3-474">Общее перечисление с помощью LINQ выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a95c3-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="a95c3-475">Перечислив оба набора строк, мы будем в цикле перебирать все строки,</span><span class="sxs-lookup"><span data-stu-id="a95c3-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="a95c3-476">выбирая для каждой строки из левого набора все строки, которые соответствуют условию, заданному для средства объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="a95c3-477">Выходные значения следует передавать в выход `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="a95c3-478">Фактический вывод данных инициируется вызовом метода `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="a95c3-479">Ниже приведен пример средства объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="a95c3-480">В этом сценарии использования мы создаем аналитический отчет для организации розничной торговли.</span><span class="sxs-lookup"><span data-stu-id="a95c3-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="a95c3-481">Наша задача — найти все товары стоимостью более 20 000 долларов США, которые за определенный промежуток времени продавались через веб-сайт быстрее, чем через обычные точки розничной торговли.</span><span class="sxs-lookup"><span data-stu-id="a95c3-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="a95c3-482">Вот основной скрипт U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a95c3-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="a95c3-483">Вы можете сравнить логику обычной инструкции JOIN и средства объединения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="a95c3-484">Пользовательское средство объединения может вызываться как новый экземпляр объекта применения.</span><span class="sxs-lookup"><span data-stu-id="a95c3-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="a95c3-485">Или с вызовом метода фабрики оболочки.</span><span class="sxs-lookup"><span data-stu-id="a95c3-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="a95c3-486">Использование пользовательских средств редукции</span><span class="sxs-lookup"><span data-stu-id="a95c3-486">Use user-defined reducers</span></span>

<span data-ttu-id="a95c3-487">U-SQL позволяет создать пользовательские средства редукции для набора строк на языке C#, используя платформу расширения для определяемых пользователем операторов и реализацию интерфейса IReducer.</span><span class="sxs-lookup"><span data-stu-id="a95c3-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="a95c3-488">Определяемые пользователем редукторы можно использовать для исключения ненужных строк в процессе извлечения (импорта) данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="a95c3-489">Также с помощью этого средства можно обрабатывать и оценивать строки и столбцы.</span><span class="sxs-lookup"><span data-stu-id="a95c3-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="a95c3-490">Оно позволяет выбрать извлекаемые строки с использованием программируемой логики.</span><span class="sxs-lookup"><span data-stu-id="a95c3-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="a95c3-491">Чтобы определить класс пользовательского средства редукции, нужно создать интерфейс `IReducer` с необязательным атрибутом `SqlUserDefinedReducer`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="a95c3-492">Этот интерфейс класса должен содержать определение, переопределяющее интерфейс объекта `IEnumerable` для набора строк.</span><span class="sxs-lookup"><span data-stu-id="a95c3-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="a95c3-493">Атрибут **SqlUserDefinedReducer** указывает, что этот тип должен быть зарегистрирован как пользовательское средство редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="a95c3-494">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="a95c3-494">This class cannot be inherited.</span></span>
<span data-ttu-id="a95c3-495">**SqlUserDefinedReducer** — это необязательный атрибут для определения пользовательских средств редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="a95c3-496">Он используется для определения свойства IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="a95c3-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="a95c3-497">bool IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="a95c3-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="a95c3-498">**true** — указывает, что это средство редукции является идемпотентным.</span><span class="sxs-lookup"><span data-stu-id="a95c3-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="a95c3-499">Основные объекты, поддерживающие программирование, — это **input** (ввод) и **output** (вывод).</span><span class="sxs-lookup"><span data-stu-id="a95c3-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="a95c3-500">Объект input используется для перечисления входных строк,</span><span class="sxs-lookup"><span data-stu-id="a95c3-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="a95c3-501">а output — для вывода строк, полученных в результате действий по редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="a95c3-502">Для перечисления входных строк мы используем метод `Row.Get`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="a95c3-503">Параметр для метода `Row.Get` — это столбец, который передается как часть класса `PRODUCE` инструкции `REDUCE` в основном скрипте U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a95c3-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="a95c3-504">Здесь необходимо использовать правильный тип данных.</span><span class="sxs-lookup"><span data-stu-id="a95c3-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="a95c3-505">Для выходных данных используйте метод `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="a95c3-506">Важно понимать, что пользовательские средства редукции возвращают только те выходные значения, которые определены в вызове метода `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="a95c3-507">Фактический вывод данных из средства редукции инициируется вызовом метода `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="a95c3-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="a95c3-508">Ниже приведен пример средства редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="a95c3-509">В этом сценарии использования средство редукции пропускает строки с пустым именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="a95c3-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="a95c3-510">Для каждой строки в наборе строк считывается каждый обязательный столбец, затем оценивается длина имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="a95c3-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="a95c3-511">Текущую строку средство передает на выход, только если длина имени пользователя превышает 0.</span><span class="sxs-lookup"><span data-stu-id="a95c3-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="a95c3-512">Ниже представлен основной скрипт U-SQL, который использует пользовательское средство редукции.</span><span class="sxs-lookup"><span data-stu-id="a95c3-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```
