---
title: "руководство по программирование aaaU SQL озере данных Azure | Документы Microsoft"
description: "Дополнительные сведения о hello набор служб в Озера данных Azure, позволяющие toocreate платформой больших данных на основе облака."
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
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="e616a-103">Руководство по программированию U-SQL</span><span class="sxs-lookup"><span data-stu-id="e616a-103">U-SQL programmability guide</span></span>

<span data-ttu-id="e616a-104">U-SQL — это специальный язык запросов для рабочих нагрузок, обрабатывающих большие данные.</span><span class="sxs-lookup"><span data-stu-id="e616a-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="e616a-105">Один из компонентов уникальные hello U-SQL — hello сочетание hello SQL-подобного декларативный язык с расширяемостью hello и программирования, предоставляемые языком C#.</span><span class="sxs-lookup"><span data-stu-id="e616a-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="e616a-106">В этом руководстве мы сосредоточиться на hello расширяемость и Программируемость языка hello U-SQL, который включен в языках C#.</span><span class="sxs-lookup"><span data-stu-id="e616a-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="e616a-107">Требования</span><span class="sxs-lookup"><span data-stu-id="e616a-107">Requirements</span></span>

<span data-ttu-id="e616a-108">Скачивание и установка [средств Azure Data Lake для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="e616a-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="e616a-109">Начало работы с U-SQL</span><span class="sxs-lookup"><span data-stu-id="e616a-109">Get started with U-SQL</span></span>  

<span data-ttu-id="e616a-110">Рассмотрим следующий скрипт U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="e616a-111">Он определяет набор строк, который называется @a, и создает набор строк, который называется @results, из @a.</span><span class="sxs-lookup"><span data-stu-id="e616a-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="e616a-112">Типы и выражения C# в скрипте U-SQL</span><span class="sxs-lookup"><span data-stu-id="e616a-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="e616a-113">Выражение U-SQL — это выражение C# в сочетании с логическими операциями U-SQL, такими как `AND`, `OR`, и `NOT`.</span><span class="sxs-lookup"><span data-stu-id="e616a-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="e616a-114">Выражения U-SQL можно использовать с инструкциями SELECT, EXTRACT, WHERE, HAVING, GROUP BY и DECLARE.</span><span class="sxs-lookup"><span data-stu-id="e616a-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="e616a-115">Например следующий скрипт hello анализирует строку значение DateTime в предложении SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="e616a-116">Hello следующий сценарий анализирует строку значение DateTime в операторе DECLARE.</span><span class="sxs-lookup"><span data-stu-id="e616a-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="e616a-117">Использование выражений C# для преобразования типов данных</span><span class="sxs-lookup"><span data-stu-id="e616a-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="e616a-118">Hello в следующем примере показано, как преобразование данных даты и времени можно сделать с помощью выражений C#.</span><span class="sxs-lookup"><span data-stu-id="e616a-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="e616a-119">В данном конкретном случае строковые данные datetime — преобразованный toostandard даты и времени с полуночи прототип времени 00:00:00.</span><span class="sxs-lookup"><span data-stu-id="e616a-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="e616a-120">Использование выражений C# для получения текущей даты</span><span class="sxs-lookup"><span data-stu-id="e616a-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="e616a-121">toopull сегодняшняя дата, можно использовать следующее выражение C# hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="e616a-122">Ниже приведен пример того, как toouse это выражение в скрипте:</span><span class="sxs-lookup"><span data-stu-id="e616a-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="e616a-123">Использование сборок .NET</span><span class="sxs-lookup"><span data-stu-id="e616a-123">Using .NET assemblies</span></span>
<span data-ttu-id="e616a-124">Модель расширяемости U-SQL во многом зависит от hello возможность tooadd пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="e616a-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="e616a-125">В настоящее время U-SQL предоставляет возможности tooadd собственные корпорации Майкрософт. Код на основе .NET (в частности, C#).</span><span class="sxs-lookup"><span data-stu-id="e616a-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="e616a-126">Однако вы также можете добавить пользовательский код, написанный на других языках .NET, например на VB.NET или F#.</span><span class="sxs-lookup"><span data-stu-id="e616a-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="e616a-127">Регистрация сборки .NET</span><span class="sxs-lookup"><span data-stu-id="e616a-127">Register a .NET assembly</span></span>

<span data-ttu-id="e616a-128">Используйте tooplace инструкции CREATE ASSEMBLY hello сборкой .NET в базу данных U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="e616a-129">После сборки в базе данных, скрипты U-SQL можно использовать эти сборки с помощью инструкции hello ССЫЛОЧНУЮ СБОРКУ.</span><span class="sxs-lookup"><span data-stu-id="e616a-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="e616a-130">Здравствуйте, как следующий код показывает tooregister сборки:</span><span class="sxs-lookup"><span data-stu-id="e616a-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="e616a-131">Здравствуйте, как следующий код показывает tooreference сборки:</span><span class="sxs-lookup"><span data-stu-id="e616a-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="e616a-132">Обратитесь к hello [инструкции по регистрации сборки](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) , рассматриваются в этом разделе более подробно.</span><span class="sxs-lookup"><span data-stu-id="e616a-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="e616a-133">Использование версий сборок</span><span class="sxs-lookup"><span data-stu-id="e616a-133">Use assembly versioning</span></span>
<span data-ttu-id="e616a-134">В настоящее время U-SQL использует hello версии платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e616a-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="e616a-135">Поэтому убедитесь, что ваши собственные совместимы с этой версии среды выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="e616a-136">Как упоминалось выше, U-SQL выполняет код в 64-разрядном формате (x64).</span><span class="sxs-lookup"><span data-stu-id="e616a-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="e616a-137">Поэтому убедитесь, что код является скомпилированных toorun на x64.</span><span class="sxs-lookup"><span data-stu-id="e616a-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="e616a-138">В противном случае возникнет ошибка Неверный формат hello, показанного выше.</span><span class="sxs-lookup"><span data-stu-id="e616a-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="e616a-139">Любой передаваемый в хранилище файл (библиотеки DLL, файлы ресурсов, включая другие среды выполнения, машинные сборки, файлы конфигурации и т. д.) не может быть более 400 МБ.</span><span class="sxs-lookup"><span data-stu-id="e616a-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="e616a-140">общий размер Hello развернутых ресурсов, либо РАЗВЕРНУТЬ РЕСУРСОВ или с помощью ссылки tooassemblies и их дополнительных файлов, не может превышать 3 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e616a-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="e616a-141">И наконец, важно помнить, что в каждой базе данных U-SQL может быть только одна версия любой сборки.</span><span class="sxs-lookup"><span data-stu-id="e616a-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="e616a-142">Например, если вам требуется версии 7 и версии 8 hello NewtonSoft Json.Net библиотеки, необходимо tooregister их в двух разных базах данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="e616a-143">Кроме того каждый сценарий может ссылаться только на tooone версии данной сборки библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="e616a-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="e616a-144">В этом отношении U-SQL соответствует hello C# сборки управления и управления версиями семантике.</span><span class="sxs-lookup"><span data-stu-id="e616a-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="e616a-145">Использование определяемых пользователем функций</span><span class="sxs-lookup"><span data-stu-id="e616a-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="e616a-146">U-SQL, определяемые пользователем функции или определяемой пользователем функции, программировании подпрограммы, которые принимают параметры, выполняют действия (например, сложные вычисления) и возвращают hello результат этого действия в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="e616a-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="e616a-147">Hello возвращаемое значение определяемой пользователем функции может быть только одна скалярная.</span><span class="sxs-lookup"><span data-stu-id="e616a-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="e616a-148">Основной скрипт U-SQL может вызывать такие функции, как и любую другую скалярную функцию C#.</span><span class="sxs-lookup"><span data-stu-id="e616a-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="e616a-149">Мы советуем инициализировать определяемые пользователем функции U-SQL как **общедоступные** (public) и **статические** (static).</span><span class="sxs-lookup"><span data-stu-id="e616a-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="e616a-150">Первый рассмотрим простой пример hello создание определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="e616a-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="e616a-151">В этом сценарии варианта использования мы должны toodetermine hello финансового периода, а именно: hello финансового квартала финансового месяца hello первого входа в систему для конкретного пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="e616a-152">Hello первый месяц финансового года hello в нашем сценарии — июнь.</span><span class="sxs-lookup"><span data-stu-id="e616a-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="e616a-153">финансовый период toocalculate, мы представляем hello следующие функции C#:</span><span class="sxs-lookup"><span data-stu-id="e616a-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="e616a-154">Она вычисляет финансовый месяц и квартал и возвращает строковое значение.</span><span class="sxs-lookup"><span data-stu-id="e616a-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="e616a-155">В июне hello первый месяц hello первого финансового квартала, мы используем «Q1:P1».</span><span class="sxs-lookup"><span data-stu-id="e616a-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="e616a-156">Для июля — "Q1:P2" и т. д.</span><span class="sxs-lookup"><span data-stu-id="e616a-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="e616a-157">Это регулярное функции C# Приносим toouse переход в данном проекте U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="e616a-158">В этом разделе представлен раздел кода hello в этом сценарии:</span><span class="sxs-lookup"><span data-stu-id="e616a-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="e616a-159">Теперь мы будем toocall этой функции из hello базовый скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="e616a-160">toodo это, мы иметь полное имя для функции hello, включая пространство имен hello, в этом случае NameSpace.Class.Function(parameter) tooprovide.</span><span class="sxs-lookup"><span data-stu-id="e616a-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="e616a-161">Ниже приведен hello базового сценария фактическое U-SQL:</span><span class="sxs-lookup"><span data-stu-id="e616a-161">Following is hello actual U-SQL base script:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="e616a-162">Ниже приведен hello выходной файл hello выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="e616a-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="e616a-163">Это простой пример использования встроенной определяемой пользователем функции в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="e616a-164">Сохранение состояния между вызовами определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="e616a-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="e616a-165">Объекты программирования C# U-SQL может быть более сложными, используя интерактивность hello кода глобальных переменных.</span><span class="sxs-lookup"><span data-stu-id="e616a-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="e616a-166">Рассмотрим следующий вариант использования бизнес-сценария hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="e616a-167">В больших организациях пользователи могут переключаться между разными внутренними приложениями,</span><span class="sxs-lookup"><span data-stu-id="e616a-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="e616a-168">включая Microsoft Dynamics CRM, Power BI и т. д.</span><span class="sxs-lookup"><span data-stu-id="e616a-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="e616a-169">Клиентам может потребоваться tooapply анализ телеметрии как пользователи могут переключаться между различными приложениями, при каком использовании hello тенденции являются и т. д.</span><span class="sxs-lookup"><span data-stu-id="e616a-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="e616a-170">Hello для бизнеса hello предназначена toooptimize использования приложения.</span><span class="sxs-lookup"><span data-stu-id="e616a-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="e616a-171">Они также может понадобиться toocombine различных приложений или конкретных подпрограммы входа.</span><span class="sxs-lookup"><span data-stu-id="e616a-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="e616a-172">tooachieve этой цели, у нас есть toodetermine идентификаторы сеансов и время запаздывания между hello последнего сеанса, которое произошло.</span><span class="sxs-lookup"><span data-stu-id="e616a-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="e616a-173">Нам нужна toofind предыдущих вход и затем назначить этот сеансы tooall входа, которые созданный toohello того же приложения.</span><span class="sxs-lookup"><span data-stu-id="e616a-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="e616a-174">Hello первой проверки является то, что базовый скрипт U-SQL не позволяет нам tooapply вычисления над уже вычисляемых столбцов, с помощью функции LAG.</span><span class="sxs-lookup"><span data-stu-id="e616a-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="e616a-175">Hello второй задачей является то, что мы tookeep hello конкретного сеанса для всех сеансов в пределах hello же периода времени.</span><span class="sxs-lookup"><span data-stu-id="e616a-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="e616a-176">toosolve эту проблему, мы используем глобальной переменной внутри раздела кода: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="e616a-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="e616a-177">Этой глобальной переменной является весь набор строк применяется toohello во время выполнения наших скрипта.</span><span class="sxs-lookup"><span data-stu-id="e616a-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="e616a-178">Ниже приведен раздел кода hello нашей программе U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="e616a-179">В этом примере показано hello глобальная переменная `static public string globalSession;` использовать внутри hello `getStampUserSession` функции и получение повторной инициализации каждого hello время сеанса, изменить параметр.</span><span class="sxs-lookup"><span data-stu-id="e616a-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="e616a-180">Базовый скрипт U-SQL Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-180">hello U-SQL base script is as follows:</span></span>

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
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="e616a-181">Функция `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` здесь вызывается в процессе hello второй памяти строк вычисления.</span><span class="sxs-lookup"><span data-stu-id="e616a-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="e616a-182">Она передает hello `UserSessionTimestamp` и возвращает hello значение до `UserSessionTimestamp` изменилось.</span><span class="sxs-lookup"><span data-stu-id="e616a-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="e616a-183">выходной файл Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="e616a-184">В этом примере демонстрируется более сложный вариант использования сценария, в которой используется глобальная переменная в раздел кода, который является набор строк применяется toohello всей памяти.</span><span class="sxs-lookup"><span data-stu-id="e616a-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="e616a-185">Использование определяемых пользователем типов данных</span><span class="sxs-lookup"><span data-stu-id="e616a-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="e616a-186">Определяемые пользователем типы или UDT — это еще одно средство, поддерживающее возможность программирования в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="e616a-187">Определяемый пользователем тип в U-SQL действует так же, как аналогичный тип в C#.</span><span class="sxs-lookup"><span data-stu-id="e616a-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="e616a-188">C# является строго типизированным языком, позволяющей hello использовать встроенные и пользовательские типы, определяемые пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="e616a-189">U-SQL не может неявно сериализации или десериализацию произвольный определяемых пользователем типов данных при передаче между вершинами в наборах строк hello определяемого пользователем ТИПА.</span><span class="sxs-lookup"><span data-stu-id="e616a-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="e616a-190">Это означает, что пользователь hello не tooprovide явного форматирования с помощью интерфейса IFormatter hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="e616a-191">Это обеспечивает U-SQL с hello сериализацию и десериализацию методов для определяемого пользователем ТИПА hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="e616a-192">Встроенные средства извлечения и outputters U-SQL в настоящее время невозможно сериализации или десериализацию tooor определяемого пользователем ТИПА данных из файлов даже при использовании набора IFormatter hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="e616a-193">Поэтому при написании файл tooa определяемого пользователем ТИПА данных с hello выходные данные инструкции или считываются с extractor, у вас есть toopass его как строку или массив байтов.</span><span class="sxs-lookup"><span data-stu-id="e616a-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="e616a-194">Затем вызовите hello сериализации и десериализации кода (то есть метод ToString() hello UDT) явно.</span><span class="sxs-lookup"><span data-stu-id="e616a-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="e616a-195">Пользовательские средства извлечения и outputters на hello другой стороны, может считывать и записывать определяемых пользователем типов.</span><span class="sxs-lookup"><span data-stu-id="e616a-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="e616a-196">Если мы попытаемся toouse определяемого пользователем ТИПА в средство ИЗВЛЕЧЕНИЯ или OUTPUTTER (из предыдущего SELECT), как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="e616a-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="e616a-197">Мы получили hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="e616a-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="e616a-198">toowork с определяемого пользователем ТИПА в outputter, либо имеются tooserialize его toostring с hello метода ToString() или создать пользовательские outputter.</span><span class="sxs-lookup"><span data-stu-id="e616a-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="e616a-199">Сейчас определяемые пользователем типы нельзя использовать в инструкции GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="e616a-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="e616a-200">Если определяемый пользователем тип используется в GROUP BY, возникает следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="e616a-201">toodefine определяемого пользователем ТИПА, нам нужно:</span><span class="sxs-lookup"><span data-stu-id="e616a-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="e616a-202">Добавьте следующие пространства имен hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="e616a-203">Добавить `Microsoft.Analytics.Interfaces`, который необходим для интерфейсов hello определяемого пользователем ТИПА.</span><span class="sxs-lookup"><span data-stu-id="e616a-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="e616a-204">Кроме того `System.IO` необходимые toodefine hello IFormatter интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="e616a-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="e616a-205">Определите определяемый пользователем тип данных с помощью атрибута SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="e616a-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="e616a-206">**SqlUserDefinedType** является определение типа в сборке в виде определяемых пользователем типов (UDT) используется toomark U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="e616a-207">свойства Hello hello атрибута отражают физические характеристики hello hello определяемого пользователем ТИПА.</span><span class="sxs-lookup"><span data-stu-id="e616a-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="e616a-208">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-208">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-209">SqlUserDefinedType является обязательным атрибутом для определяемых пользователем типов данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="e616a-210">Конструктор Hello hello класса:</span><span class="sxs-lookup"><span data-stu-id="e616a-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="e616a-211">SqlUserDefinedTypeAttribute (модуль форматирования).</span><span class="sxs-lookup"><span data-stu-id="e616a-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="e616a-212">Модуль форматирования: требуется параметр toodefine форматирования определяемого пользователем ТИПА данных — в частности, тип hello hello `IFormatter` интерфейса должен быть передан здесь.</span><span class="sxs-lookup"><span data-stu-id="e616a-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="e616a-213">Типичные определяемого пользователем ТИПА также требует определение интерфейса IFormatter hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="e616a-214">Hello `IFormatter` интерфейс сериализует и десериализует граф объектов с типом корневого hello \<typeparamref name = «T» >.</span><span class="sxs-lookup"><span data-stu-id="e616a-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="e616a-215">\<typeparam name = «T» > Здравствуйте корневом типе для hello объекта графа tooserialize и десериализацию.</span><span class="sxs-lookup"><span data-stu-id="e616a-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="e616a-216">**Выполнить десериализацию**: десериализуются hello данные на hello предоставленный поток и воспроизводит hello граф объектов.</span><span class="sxs-lookup"><span data-stu-id="e616a-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="e616a-217">**Сериализовать**: сериализует объект или граф объектов с hello заданному корневой toohello предоставленный поток.</span><span class="sxs-lookup"><span data-stu-id="e616a-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="e616a-218">`MyType`экземпляр: экземпляр типа hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="e616a-219">`IColumnWriter`модуль записи или `IColumnReader` чтения: hello базовый поток столбца.</span><span class="sxs-lookup"><span data-stu-id="e616a-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="e616a-220">`ISerializationContext`Контекст: перечисление, которое определяет набор флагов, указывающее hello исходный или целевой контекст для потока hello во время сериализации.</span><span class="sxs-lookup"><span data-stu-id="e616a-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="e616a-221">**Промежуточные**: Указывает, что исходный или целевой контекст hello не материализованного хранилища.</span><span class="sxs-lookup"><span data-stu-id="e616a-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="e616a-222">**Сохраняемости**: Указывает, что исходный или целевой контекст hello материализованного хранилища.</span><span class="sxs-lookup"><span data-stu-id="e616a-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="e616a-223">Как и обычный тип C#, определение определяемого пользователем типа данных в U-SQL может переопределять такие операторы, как +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="e616a-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="e616a-224">Также оно может содержать статические методы.</span><span class="sxs-lookup"><span data-stu-id="e616a-224">It can also include static methods.</span></span> <span data-ttu-id="e616a-225">Например, если мы будем toouse данного определяемого пользователем ТИПА как параметра tooa Агрегатная функция MIN U-SQL, у нас есть toodefine < переопределение оператора.</span><span class="sxs-lookup"><span data-stu-id="e616a-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="e616a-226">Ранее в этом руководстве мы показали пример для финансового периода код из hello определенную дату в формате hello Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="e616a-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="e616a-227">Следующий пример Hello показано как toodefine пользовательского ввода для значения финансового периода.</span><span class="sxs-lookup"><span data-stu-id="e616a-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="e616a-228">Ниже приведен пример раздела кода программной части с определяемым пользователем типом данных и интерфейсом IFormatter.</span><span class="sxs-lookup"><span data-stu-id="e616a-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="e616a-229">Hello определенный тип включает два числа: квартал и месяц.</span><span class="sxs-lookup"><span data-stu-id="e616a-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="e616a-230">Здесь определены операторы ==, ! =, >, < и статический метод ToString().</span><span class="sxs-lookup"><span data-stu-id="e616a-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="e616a-231">Как упоминалось выше, определяемый пользователем тип данных можно использовать в выражениях SELECT, но нельзя — в средствах OUTPUTTER и EXTRACTOR без настраиваемой сериализации.</span><span class="sxs-lookup"><span data-stu-id="e616a-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="e616a-232">Она либо содержит toobe сериализованы в виде строки с ToString() или использовать с пользовательской OUTPUTTER и ИЗВЛЕЧЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="e616a-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="e616a-233">Теперь давайте рассмотрим, как можно применять определяемый пользователем тип данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="e616a-234">В разделе кода мы изменили нашей GetFiscalPeriod функция toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="e616a-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="e616a-235">Как видите, он возвращает значение hello нашей FiscalPeriod типа.</span><span class="sxs-lookup"><span data-stu-id="e616a-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="e616a-236">Здесь мы предлагаем примером как toouse, расположенным в базовый скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="e616a-237">В этом примере представлено несколько способов вызова определяемого пользователем типа данных из скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="e616a-238">Ниже приведен пример полного раздела кода программной части.</span><span class="sxs-lookup"><span data-stu-id="e616a-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="e616a-239">Использование определяемых пользователем статистических функций</span><span class="sxs-lookup"><span data-stu-id="e616a-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="e616a-240">Определяемые пользователем статистические выражения — это любые функции статистической обработки, не входящие в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="e616a-241">пример Hello можно статистические tooperform пользовательских математических вычислений, конкатенации строк манипуляций со строками и т. д.</span><span class="sxs-lookup"><span data-stu-id="e616a-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="e616a-242">определение определяемой пользователем статистической базового класса Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="e616a-243">**SqlUserDefinedAggregate** указывает, что тип hello должен быть зарегистрирован как определяемой пользователем статистической функции.</span><span class="sxs-lookup"><span data-stu-id="e616a-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="e616a-244">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-244">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-245">Атрибут SqlUserDefinedType является **необязательным** для определяемого пользователем статистического выражения.</span><span class="sxs-lookup"><span data-stu-id="e616a-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="e616a-246">Hello базового класса позволяет абстрактные параметры toopass трех: два входных параметров и один — как результат hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="e616a-247">типы данных Hello переменной и должен быть определен во время наследования классов.</span><span class="sxs-lookup"><span data-stu-id="e616a-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="e616a-248">**Init** — метод, который вызывается один раз для каждой группы во время вычисления.</span><span class="sxs-lookup"><span data-stu-id="e616a-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="e616a-249">Он предоставляет процедуры инициализации для каждой группы статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="e616a-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="e616a-250">**Accumulate** — метод, который выполняется один раз для каждого значения.</span><span class="sxs-lookup"><span data-stu-id="e616a-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="e616a-251">Он предоставляет основные функции hello для hello статистического алгоритма.</span><span class="sxs-lookup"><span data-stu-id="e616a-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="e616a-252">Это может быть используется tooaggregate значения с различными типами данных, которые определены во время наследования классов.</span><span class="sxs-lookup"><span data-stu-id="e616a-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="e616a-253">Он может принимать два параметра разных типов данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="e616a-254">**Завершение** выполняется один раз на каждую группу статистической обработки в конце hello обработки toooutput hello результат для каждой группы.</span><span class="sxs-lookup"><span data-stu-id="e616a-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="e616a-255">Используйте определение класса hello toodeclare правильные входные данные и типов выходных данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="e616a-256">T1: Первый параметр tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="e616a-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="e616a-257">T2: Первый параметр tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="e616a-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="e616a-258">TResult — возвращаемый тип для метода Terminate.</span><span class="sxs-lookup"><span data-stu-id="e616a-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="e616a-259">Например:</span><span class="sxs-lookup"><span data-stu-id="e616a-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="e616a-260">или</span><span class="sxs-lookup"><span data-stu-id="e616a-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="e616a-261">Использование определяемых пользователем статистических выражений в U-SQL</span><span class="sxs-lookup"><span data-stu-id="e616a-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="e616a-262">toouse определяемой пользователем статистической функции, сначала его определения в коде или сослаться на нее из существующих программирования hello DLL как было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="e616a-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="e616a-263">Затем используйте hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="e616a-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="e616a-264">Ниже приведен пример определяемого пользователем статистического выражения.</span><span class="sxs-lookup"><span data-stu-id="e616a-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="e616a-265">И основной скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="e616a-266">В этом сценарии варианта использования мы объединения GUID классов для конкретных пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="e616a-267">Использование определяемых пользователем объектов</span><span class="sxs-lookup"><span data-stu-id="e616a-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="e616a-268">U-SQL позволяет toodefine программирование пользовательских объектов, которые называются определенных пользователем объектов или определяемого пользователем ОПЕРАТОРА.</span><span class="sxs-lookup"><span data-stu-id="e616a-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="e616a-269">Hello ниже приведен список определяемого пользователем ОПЕРАТОРА в U-SQL:</span><span class="sxs-lookup"><span data-stu-id="e616a-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="e616a-270">Пользовательские средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="e616a-270">User-defined extractors</span></span>
    * <span data-ttu-id="e616a-271">Извлечение по строкам.</span><span class="sxs-lookup"><span data-stu-id="e616a-271">Extract row by row</span></span>
    * <span data-ttu-id="e616a-272">Использовать tooimplement извлечения данных из пользовательских структурированных файлов</span><span class="sxs-lookup"><span data-stu-id="e616a-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="e616a-273">Пользовательские средства вывода.</span><span class="sxs-lookup"><span data-stu-id="e616a-273">User-defined outputters</span></span>
    * <span data-ttu-id="e616a-274">Вывод по строкам.</span><span class="sxs-lookup"><span data-stu-id="e616a-274">Output row by row</span></span>
    * <span data-ttu-id="e616a-275">Использовать toooutput пользовательских типов данных или настраиваемые форматы файлов</span><span class="sxs-lookup"><span data-stu-id="e616a-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="e616a-276">Пользовательские средства обработки.</span><span class="sxs-lookup"><span data-stu-id="e616a-276">User-defined processors</span></span>
    * <span data-ttu-id="e616a-277">Получение одной строки и возврат одной строки.</span><span class="sxs-lookup"><span data-stu-id="e616a-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="e616a-278">Используется tooreduce hello числа столбцов и создают новые столбцы со значениями, которые являются производными от существующего набора столбцов</span><span class="sxs-lookup"><span data-stu-id="e616a-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="e616a-279">Пользовательские средства применения.</span><span class="sxs-lookup"><span data-stu-id="e616a-279">User-defined appliers</span></span>
    * <span data-ttu-id="e616a-280">Принимает одну строку и создает toon строк: 0</span><span class="sxs-lookup"><span data-stu-id="e616a-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="e616a-281">Использование с инструкциями OUTER и CROSS APPLY.</span><span class="sxs-lookup"><span data-stu-id="e616a-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="e616a-282">Пользовательские средства объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-282">User-defined combiners</span></span>
    * <span data-ttu-id="e616a-283">Объединяют наборы строк — определяемые пользователем инструкции JOIN.</span><span class="sxs-lookup"><span data-stu-id="e616a-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="e616a-284">Пользовательские средства редукции.</span><span class="sxs-lookup"><span data-stu-id="e616a-284">User-defined reducers</span></span>
    * <span data-ttu-id="e616a-285">Получение n строк и возврат одной строки.</span><span class="sxs-lookup"><span data-stu-id="e616a-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="e616a-286">Использовать tooreduce hello число строк</span><span class="sxs-lookup"><span data-stu-id="e616a-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="e616a-287">Определяемый пользователем ОПЕРАТОР обычно вызывается явным образом в скрипт U-SQL в составе приветствия, следующие инструкции U-SQL:</span><span class="sxs-lookup"><span data-stu-id="e616a-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="e616a-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="e616a-288">EXTRACT</span></span>
* <span data-ttu-id="e616a-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="e616a-289">OUTPUT</span></span>
* <span data-ttu-id="e616a-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="e616a-290">PROCESS</span></span>
* <span data-ttu-id="e616a-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="e616a-291">COMBINE</span></span>
* <span data-ttu-id="e616a-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="e616a-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="e616a-293">Определяемый пользователем ОПЕРАТОР являются ограниченные tooconsume 0,5 ГБ памяти.</span><span class="sxs-lookup"><span data-stu-id="e616a-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="e616a-294">Это ограничение памяти применяется toolocal выполнений.</span><span class="sxs-lookup"><span data-stu-id="e616a-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="e616a-295">Использование пользовательских средств извлечения</span><span class="sxs-lookup"><span data-stu-id="e616a-295">Use user-defined extractors</span></span>
<span data-ttu-id="e616a-296">U-SQL позволяет tooimport внешних данных с помощью инструкции ИЗВЛЕЧЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="e616a-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="e616a-297">Инструкция EXTRACT может использовать встроенные средства извлечения для определяемых пользователем объектов.</span><span class="sxs-lookup"><span data-stu-id="e616a-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="e616a-298">*Extractors.Text()*: извлекает данные из текстовых файлов с разделителями в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="e616a-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="e616a-299">*Extractors.Csv()*: извлекает данные из файлов данных с разделителями-запятыми (CSV) в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="e616a-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="e616a-300">*Extractors.Csv()*: извлекает данные из файлов со значением с разделением знаками табуляции (TSV), в разных кодировках.</span><span class="sxs-lookup"><span data-stu-id="e616a-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="e616a-301">Это может быть полезным toodevelop пользовательские извлечения.</span><span class="sxs-lookup"><span data-stu-id="e616a-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="e616a-302">Это может оказаться полезным во время импорта данных Если мы хотим toodo любой hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e616a-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="e616a-303">Изменить входные данные, разделяя столбцы или изменяя отдельные значения.</span><span class="sxs-lookup"><span data-stu-id="e616a-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="e616a-304">Hello функциональности ПРОЦЕССОРОВ лучше подходит для объединения столбцов.</span><span class="sxs-lookup"><span data-stu-id="e616a-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="e616a-305">Выполнить синтаксический анализ неструктурированных данных, например веб-страниц или сообщений электронной почты, или частично структурированных данных, например документов XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="e616a-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="e616a-306">Выполнить анализ данных в неподдерживаемых кодировках.</span><span class="sxs-lookup"><span data-stu-id="e616a-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="e616a-307">toodefine извлечения, определяемых пользователем, или Включить, нам нужно toocreate `IExtractor` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="e616a-308">Все входные параметры извлечения toohello, например разделителей столбцов или строк, а также кодирование, должны toobe, определенные в hello конструктор класса hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="e616a-309">Hello `IExtractor` интерфейс также должен содержать определение для hello `IEnumerable<IRow>` переопределить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="e616a-310">Hello **SqlUserDefinedExtractor** атрибут указывает, что hello тип должен быть зарегистрирован как извлечение, определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="e616a-311">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-311">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-312">SqlUserDefinedExtractor — это необязательный атрибут для определения пользовательского средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="e616a-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="e616a-313">Он используется toodefine AtomicFileProcessing свойство для объекта ЛЮЧИТЬ hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="e616a-314">bool AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="e616a-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="e616a-315">Значение **true** указывает, что это средство извлечения требует атомарные входные файлы (JSON, XML и другие).</span><span class="sxs-lookup"><span data-stu-id="e616a-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="e616a-316">Значение **false** указывает, что это средство извлечения умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).</span><span class="sxs-lookup"><span data-stu-id="e616a-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="e616a-317">Hello основные ЛЮЧИТЬ программные объекты не **ввода** и **вывода**.</span><span class="sxs-lookup"><span data-stu-id="e616a-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e616a-318">Hello входной объект — входных данных используется tooenumerate как `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="e616a-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="e616a-319">Hello выходной объект — используется tooset выходных данных в результате действия извлечения hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="e616a-320">Hello входных данных осуществляется с помощью `System.IO.Stream` и `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="e616a-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="e616a-321">Перечисление входных столбцов мы сначала разделить hello входного потока с помощью разделителя строки.</span><span class="sxs-lookup"><span data-stu-id="e616a-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="e616a-322">Затем еще раз разбиваем входную строку на столбцы:</span><span class="sxs-lookup"><span data-stu-id="e616a-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="e616a-323">tooset выходные данные, мы используем hello `output.Set` метод.</span><span class="sxs-lookup"><span data-stu-id="e616a-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="e616a-324">Очень важно, что toounderstand, hello пользовательские средства извлечения только выводит столбцов и значений, определенных с выводом hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="e616a-325">Вызов метода Set:</span><span class="sxs-lookup"><span data-stu-id="e616a-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="e616a-326">выходные данные фактического извлечения Hello инициируется путем вызова `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e616a-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e616a-327">Ниже приведен пример hello извлечения:</span><span class="sxs-lookup"><span data-stu-id="e616a-327">Following is hello extractor example:</span></span>

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
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
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
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
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

<span data-ttu-id="e616a-328">В этом сценарии варианта использования извлечения hello повторно формирует hello GUID для столбца «guid» и преобразует значения hello случая tooupper столбца «пользователь».</span><span class="sxs-lookup"><span data-stu-id="e616a-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="e616a-329">Пользовательские средства извлечения могут создавать более сложные результаты, анализируя входные данные и преобразовывая их.</span><span class="sxs-lookup"><span data-stu-id="e616a-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="e616a-330">Ниже представлен основной скрипт U-SQL, который использует пользовательское средство извлечения.</span><span class="sxs-lookup"><span data-stu-id="e616a-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="e616a-331">Использование пользовательских средств вывода</span><span class="sxs-lookup"><span data-stu-id="e616a-331">Use user-defined outputters</span></span>
<span data-ttu-id="e616a-332">Определяемые пользователем outputter является другой UDO U-SQL, который позволяет вам tooextend встроенные функциональные возможности U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="e616a-333">Аналогичные toohello извлечения, существует несколько встроенных outputters.</span><span class="sxs-lookup"><span data-stu-id="e616a-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="e616a-334">*Outputters.Text()*: Записывает текстовые файлы с разными кодировками toodelimited данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="e616a-335">*Outputters.Csv()*: записывает данные toocomma-запятыми (CSV) файлы различных кодировок.</span><span class="sxs-lookup"><span data-stu-id="e616a-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="e616a-336">*Outputters.Tsv()*: записывает запятыми tootab данных файлов (TSV) различных кодировок.</span><span class="sxs-lookup"><span data-stu-id="e616a-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="e616a-337">Пользовательские outputter позволяет toowrite данных в пользовательском формате определенных.</span><span class="sxs-lookup"><span data-stu-id="e616a-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="e616a-338">Это может быть полезно для hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e616a-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="e616a-339">Запись данных toosemi структурированных и неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="e616a-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="e616a-340">Запись данных в неподдерживаемых кодировках.</span><span class="sxs-lookup"><span data-stu-id="e616a-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="e616a-341">Преобразование выходных данных или добавление пользовательских атрибутов.</span><span class="sxs-lookup"><span data-stu-id="e616a-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="e616a-342">toodefine outputter определяемых пользователем, нам нужно toocreate hello `IOutputter` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="e616a-343">Ниже приведен базовый hello `IOutputter` реализацию класса:</span><span class="sxs-lookup"><span data-stu-id="e616a-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="e616a-344">Все входные параметры toohello outputter, например разделителей столбцов или строк, кодировки и т. д., должны toobe, определенные в hello конструктор класса hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="e616a-345">Hello `IOutputter` интерфейс также должен содержать определение для `void Output` переопределения.</span><span class="sxs-lookup"><span data-stu-id="e616a-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="e616a-346">атрибут Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` при необходимости можно задать для обработки файла atomic.</span><span class="sxs-lookup"><span data-stu-id="e616a-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="e616a-347">Дополнительные сведения см. в разделе hello, приведенные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="e616a-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="e616a-348">Метод `Output` вызывается для каждой входной строки.</span><span class="sxs-lookup"><span data-stu-id="e616a-348">`Output` is called for each input row.</span></span> <span data-ttu-id="e616a-349">Он возвращает hello `IUnstructuredWriter output` набора строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="e616a-350">используется Hello конструктор класса outputter toopass параметры toohello определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="e616a-351">`Close`используется toooptionally переопределить состояние дорогих toorelease или определить, когда была сделана последняя строка hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="e616a-352">**SqlUserDefinedOutputter** атрибут указывает, что hello тип должен быть зарегистрирован как outputter, определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="e616a-353">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-353">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-354">SqlUserDefinedOutputter — это необязательный атрибут для определения пользовательских средств вывода.</span><span class="sxs-lookup"><span data-stu-id="e616a-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="e616a-355">Оно использовалось свойство AtomicFileProcessing toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="e616a-356">bool AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="e616a-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="e616a-357">**true** — указывает, что это средство вывода требует атомарные выходные файлы (JSON, XML и другие).</span><span class="sxs-lookup"><span data-stu-id="e616a-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="e616a-358">**false** — указывает, что это средство вывода умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).</span><span class="sxs-lookup"><span data-stu-id="e616a-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="e616a-359">Программирование основных объектов Hello **строки** и **вывода**.</span><span class="sxs-lookup"><span data-stu-id="e616a-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="e616a-360">Hello **строки** объект является используемым tooenumerate выходные данные как `IRow` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="e616a-361">**Выходные данные** используется tooset вывод данных toohello целевой файл.</span><span class="sxs-lookup"><span data-stu-id="e616a-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="e616a-362">Hello выходных данных осуществляется с помощью hello `IRow` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="e616a-363">Выходные данные передаются построчно.</span><span class="sxs-lookup"><span data-stu-id="e616a-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="e616a-364">с помощью метода Get hello интерфейса IRow hello перечисляются Hello отдельных значений:</span><span class="sxs-lookup"><span data-stu-id="e616a-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="e616a-365">Имена отдельных столбцов можно определить с помощью вызова метода `row.Schema`.</span><span class="sxs-lookup"><span data-stu-id="e616a-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e616a-366">Такой подход позволяет toobuild гибкие outputter для любой схемы метаданных.</span><span class="sxs-lookup"><span data-stu-id="e616a-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="e616a-367">Hello выходные данные записываются toofile с помощью `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="e616a-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="e616a-368">параметр потока Hello задано слишком`output.BaseStrea` как часть `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="e616a-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="e616a-369">Обратите внимание, что файл toohello буфера данных важно tooflush hello после каждой итерации строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="e616a-370">Кроме того, hello `StreamWriter` объект должен использоваться с hello удаляемого атрибута включен (по умолчанию) и hello **с помощью** ключевое слово:</span><span class="sxs-lookup"><span data-stu-id="e616a-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="e616a-371">В противном случае — после каждой итерации вызывайте явным образом метод Flush().</span><span class="sxs-lookup"><span data-stu-id="e616a-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="e616a-372">Это демонстрируется в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="e616a-373">Установка колонтитулов для пользовательского средства вывода</span><span class="sxs-lookup"><span data-stu-id="e616a-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="e616a-374">tooset заголовок, используйте одну итерацию потока выполнения.</span><span class="sxs-lookup"><span data-stu-id="e616a-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="e616a-375">Сначала Hello кода в hello `if (isHeaderRow)` блок выполняется только один раз.</span><span class="sxs-lookup"><span data-stu-id="e616a-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="e616a-376">Для нижнего колонтитула hello, используйте экземпляр ссылок toohello hello `System.IO.Stream` объекта (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="e616a-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="e616a-377">Запись hello нижнего колонтитула в hello метод Close() hello `IOutputter` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="e616a-378">(Дополнительные сведения см. следующий пример hello.)</span><span class="sxs-lookup"><span data-stu-id="e616a-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="e616a-379">Ниже приведен пример пользовательского средства вывода.</span><span class="sxs-lookup"><span data-stu-id="e616a-379">Following is an example of a user-defined outputter:</span></span>

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

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
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
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
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
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="e616a-380">И основной скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-380">And U-SQL base script:</span></span>

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
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="e616a-381">Это средство вывода для формата HTML. Оно создает HTML-файл с данными таблицы.</span><span class="sxs-lookup"><span data-stu-id="e616a-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="e616a-382">Вызов средства вывода из основного скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="e616a-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="e616a-383">toocall пользовательские outputter из hello базовый скрипт U-SQL, новый экземпляр объекта outputter hello hello имеет toobe создан.</span><span class="sxs-lookup"><span data-stu-id="e616a-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="e616a-384">tooavoid создание экземпляра hello объекта в скрипте базового, можно создать оболочку функции, как показано в примере выше:</span><span class="sxs-lookup"><span data-stu-id="e616a-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="e616a-385">В этом случае исходного вызова hello выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="e616a-386">Использование пользовательских средств обработки</span><span class="sxs-lookup"><span data-stu-id="e616a-386">Use user-defined processors</span></span>
<span data-ttu-id="e616a-387">Определяемые пользователем процессора или UDP, — это тип определяемого пользователем ОПЕРАТОРА U-SQL, позволяющий tooprocess hello входящих строк, применяя возможности программирования.</span><span class="sxs-lookup"><span data-stu-id="e616a-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="e616a-388">UDP позволяет toocombine столбцы, изменить значения, а при необходимости, добавить новые столбцы.</span><span class="sxs-lookup"><span data-stu-id="e616a-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="e616a-389">По сути это помогает tooprocess элементы набора строк tooproduce необходимых данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="e616a-390">toodefine UDP, нам нужно toocreate `IProcessor` интерфейс с hello `SqlUserDefinedProcessor` атрибут, который является необязательным для протокола UDP.</span><span class="sxs-lookup"><span data-stu-id="e616a-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="e616a-391">Этот интерфейс должен содержать определение hello hello `IRow` переопределить интерфейс набора строк, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="e616a-392">**SqlUserDefinedProcessor** указывает, что hello тип должен быть зарегистрирован как процессор определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="e616a-393">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-393">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-394">атрибут Hello SqlUserDefinedProcessor **необязательно** для определения UDP.</span><span class="sxs-lookup"><span data-stu-id="e616a-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="e616a-395">Основные возможности программирования объектов Hello **входной** и **вывода**.</span><span class="sxs-lookup"><span data-stu-id="e616a-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e616a-396">Hello входной объект — используется tooenumerate входные столбцы и выходные данные и tooset выходных данных в результате hello загруженности процессора.</span><span class="sxs-lookup"><span data-stu-id="e616a-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="e616a-397">Для перечисления входные столбцы, мы используем hello `input.Get` метод.</span><span class="sxs-lookup"><span data-stu-id="e616a-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="e616a-398">Здравствуйте, параметр `input.Get` метод — столбец, который передается как часть hello `PRODUCE` предложения hello `PROCESS` инструкции базового сценария hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="e616a-399">Мы должны toouse hello верный тип данных, здесь.</span><span class="sxs-lookup"><span data-stu-id="e616a-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="e616a-400">Для выходных данных, используйте hello `output.Set` метод.</span><span class="sxs-lookup"><span data-stu-id="e616a-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="e616a-401">Очень важно toonote этой пользовательской производитель выводит только столбцы и значения, определенные с hello `output.Set` вызова метода.</span><span class="sxs-lookup"><span data-stu-id="e616a-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="e616a-402">выходные данные процессора Hello инициируется путем вызова `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e616a-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e616a-403">Ниже приведен пример использования средства обработки.</span><span class="sxs-lookup"><span data-stu-id="e616a-403">Following is a processor example:</span></span>

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

<span data-ttu-id="e616a-404">В этом сценарии варианта использования процессора hello создает новый столбец с именем «full_description», объединяя hello существующие столбцы — в этом случае «user» в верхнем регистре, а «des».</span><span class="sxs-lookup"><span data-stu-id="e616a-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="e616a-405">Он также повторно формирует идентификатор GUID и возвращает hello исходные и новые значения GUID.</span><span class="sxs-lookup"><span data-stu-id="e616a-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="e616a-406">Как видно из предыдущего примера hello, можно вызывать методы C# во время `output.Set` вызова метода.</span><span class="sxs-lookup"><span data-stu-id="e616a-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="e616a-407">Ниже приведен пример основного скрипта U-SQL, использующего пользовательское средство обработки.</span><span class="sxs-lookup"><span data-stu-id="e616a-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="e616a-408">Использование пользовательских средств применения</span><span class="sxs-lookup"><span data-stu-id="e616a-408">Use user-defined appliers</span></span>
<span data-ttu-id="e616a-409">Объект применения пользовательских U-SQL включает функции tooinvoke пользовательские C# для каждой строки, возвращаемой внешним табличным выражением запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="e616a-410">Hello правый вход оценивается для каждой строки из левого входа hello и объединяются для конечного результата hello hello строки, которые будут созданы.</span><span class="sxs-lookup"><span data-stu-id="e616a-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="e616a-411">Список столбцов, созданных оператором APPLY hello Hello представляют Привет сочетание hello набор столбцов в hello влево и вправо ввода hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="e616a-412">Объект применения пользовательских вызывается как часть выражения USQL SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="e616a-413">Здравствуйте, типичный вызов toohello определяемого пользователем объекта применения выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="e616a-414">Дополнительные сведения об использовании средств применения в выражении SELECT см. в статье [U-SQL SELECT, выбрав из CROSS APPLY и OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="e616a-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="e616a-415">Hello определяемого пользователем объекта применения определение базового класса выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="e616a-416">toodefine применения, определяемых пользователем, нам нужно toocreate hello `IApplier` интерфейс с hello [`SqlUserDefinedApplier`] атрибута, который не является обязательным для применения определение определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="e616a-417">Применить вызывается для каждой строки внешней таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="e616a-418">Он возвращает hello `IUpdatableRow` вывода набора строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="e616a-419">Класс конструктора Hello — применения пользовательских toohello используется toopass параметров.</span><span class="sxs-lookup"><span data-stu-id="e616a-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="e616a-420">**SqlUserDefinedApplier** указывает, что hello тип должен быть зарегистрирован как объект применения определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="e616a-421">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-421">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-422">Атрибут **SqlUserDefinedApplier** является **необязательным** для определения пользовательского средства применения.</span><span class="sxs-lookup"><span data-stu-id="e616a-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="e616a-423">Существуют следующие основные возможности программирования объектов Hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="e616a-424">Входной набор строк передается в виде ввода `IRow`.</span><span class="sxs-lookup"><span data-stu-id="e616a-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="e616a-425">Hello выходные строки будут создаваться как `IUpdatableRow` интерфейс вывода.</span><span class="sxs-lookup"><span data-stu-id="e616a-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="e616a-426">Имен отдельных столбцов можно определить с помощью вызывающему Привет `IRow` метод схемы.</span><span class="sxs-lookup"><span data-stu-id="e616a-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e616a-427">tooget hello фактическими значениями данных из входящего hello `IRow`, мы используем метод Get() hello `IRow` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="e616a-428">Или, рекомендуется использовать имя столбца схемы hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="e616a-429">Hello выходного значения должны задаваться с `IUpdatableRow` выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e616a-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="e616a-430">Это важные toounderstand, пользовательские значения выводить только столбцы и значения, определенные с `output.Set` вызова метода.</span><span class="sxs-lookup"><span data-stu-id="e616a-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="e616a-431">Фактический выход Hello инициируется путем вызова `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e616a-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e616a-432">Конструктор toohello могут передаваться Hello определяемого пользователем объекта применения параметров.</span><span class="sxs-lookup"><span data-stu-id="e616a-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="e616a-433">Объект применения может возвращать переменное число столбцов, которые должны toobe, определенные во время вызова объекта применения hello в базовый скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="e616a-434">Ниже приведен пример применения пользовательских hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="e616a-435">Ниже приведен hello базовый скрипт U-SQL для применения этой определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="e616a-436">В этом сценарии вариантов использования определяемых пользователем зарегистрированную действует как средство синтаксического анализа значения с разделителями запятыми для hello автомобиля парка свойства.</span><span class="sxs-lookup"><span data-stu-id="e616a-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="e616a-437">строки входной файл Hello выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="e616a-438">Это стандартный TSV-файл со значениями с разделением знаками табуляции, в котором столбец свойств содержит такие свойства автомобилей, как производитель, модель и т. д.</span><span class="sxs-lookup"><span data-stu-id="e616a-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="e616a-439">Эти свойства должны быть проанализированный toohello столбцов таблицы.</span><span class="sxs-lookup"><span data-stu-id="e616a-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="e616a-440">Hello применения, который предоставляется также позволяет toogenerate динамического количество свойств в hello привести набора строк, на основе параметра hello, которое передается.</span><span class="sxs-lookup"><span data-stu-id="e616a-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="e616a-441">Вы можете создать либо все свойства, либо определенный набор свойств.</span><span class="sxs-lookup"><span data-stu-id="e616a-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="e616a-442">Объект применения пользовательских Hello можно вызвать как новый экземпляр объекта применения:</span><span class="sxs-lookup"><span data-stu-id="e616a-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="e616a-443">Или с вызовом hello заводского метода оболочки:</span><span class="sxs-lookup"><span data-stu-id="e616a-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="e616a-444">Использование пользовательских средств объединения</span><span class="sxs-lookup"><span data-stu-id="e616a-444">Use user-defined combiners</span></span>
<span data-ttu-id="e616a-445">Определяемые пользователем функции объединения или UDC, позволяет toocombine строки из левой и правой наборы строк на основе пользовательской логики.</span><span class="sxs-lookup"><span data-stu-id="e616a-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="e616a-446">Пользовательское средство объединения используется с выражением COMBINE.</span><span class="sxs-lookup"><span data-stu-id="e616a-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="e616a-447">Функции объединения вызывается с hello ОБЪЕДИНЕНИЕ выражение, которое предоставляет hello необходимые сведения об обоих входных наборов строк hello, Группировка столбцов, hello hello ожидаемый результат схемы и Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="e616a-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="e616a-448">toocall функции объединения в базовый скрипт U-SQL, мы используем hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="e616a-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="e616a-449">Дополнительные сведения см. в [описании выражения COMBINE для U-SQL](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="e616a-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="e616a-450">toodefine определяемой пользователем функции объединения, нам нужно toocreate hello `ICombiner` интерфейс с hello [`SqlUserDefinedCombiner`] атрибута, который является необязательным для определения определяемой пользователем функции объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="e616a-451">Определение базового класса `ICombiner`.</span><span class="sxs-lookup"><span data-stu-id="e616a-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="e616a-452">Здравствуйте, пользовательская реализация `ICombiner` интерфейс должен содержать определение hello для `IEnumerable<IRow>` объединить переопределения.</span><span class="sxs-lookup"><span data-stu-id="e616a-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="e616a-453">Hello **SqlUserDefinedCombiner** атрибут указывает, что тип hello должен быть зарегистрирован как определяемые пользователем функции объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="e616a-454">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-454">This class cannot be inherited.</span></span>

<span data-ttu-id="e616a-455">**SqlUserDefinedCombiner** — свойство режима используется toodefine hello функции объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="e616a-456">Он является необязательным атрибутом для определения пользовательских средств объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="e616a-457">Режимы CombinerMode</span><span class="sxs-lookup"><span data-stu-id="e616a-457">CombinerMode     Mode</span></span>

<span data-ttu-id="e616a-458">Перечисление CombinerMode может занять hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="e616a-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="e616a-459">Full (0), потенциально зависит от всех hello входные строки из каждой строки вывода влево и вправо, с hello же значение ключа.</span><span class="sxs-lookup"><span data-stu-id="e616a-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="e616a-460">Left (1), каждая строка выходных данных зависит от одной входной строки слева hello (и потенциально все строки из hello справа с hello же значение ключа).</span><span class="sxs-lookup"><span data-stu-id="e616a-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="e616a-461">Каждая строка выходных данных зависит от одной входной строки из правой hello вправо (2) (и потенциально все строки из левой hello с hello же значение ключа).</span><span class="sxs-lookup"><span data-stu-id="e616a-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="e616a-462">Внутренний (3), каждая строка выходных данных зависит от один входной строки из левой и правой части hello же значение.</span><span class="sxs-lookup"><span data-stu-id="e616a-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="e616a-463">Пример: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="e616a-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="e616a-464">Программирование основных объектов Hello являются:</span><span class="sxs-lookup"><span data-stu-id="e616a-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="e616a-465">Входные наборы строк передаются в виде левого (**left**) и правого (**right**) интерфейсов типа `IRowset`.</span><span class="sxs-lookup"><span data-stu-id="e616a-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="e616a-466">Они должны быть перечислены для обработки.</span><span class="sxs-lookup"><span data-stu-id="e616a-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="e616a-467">Можно выполнять только перечисление каждого интерфейса один раз, поэтому мы tooenumerate и кэшировать его при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e616a-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="e616a-468">Для целей кэширования мы можем создать тип структуры памяти List\<T\> как результат выполнения запроса LINQ, в частности создать тип List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="e616a-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="e616a-469">во время перечисления также можно использовать анонимные данные типа Hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="e616a-470">В разделе [введение tooLINQ запросов (C#)](https://msdn.microsoft.com/library/bb397906.aspx) Дополнительные сведения о запросах LINQ и [IEnumerable\<T\> интерфейс](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) Дополнительные сведения о IEnumerable\<T\> интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="e616a-471">tooget hello фактическими значениями данных из входящего hello `IRowset`, мы используем метод Get() hello `IRow` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e616a-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="e616a-472">Имен отдельных столбцов можно определить с помощью вызывающему Привет `IRow` метод схемы.</span><span class="sxs-lookup"><span data-stu-id="e616a-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e616a-473">Или с помощью hello имя столбца схемы:</span><span class="sxs-lookup"><span data-stu-id="e616a-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="e616a-474">Hello общие перечисления с помощью LINQ выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e616a-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="e616a-475">После перебора обоих наборов строк, мы будем tooloop всех строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="e616a-476">Для каждой строки в наборе строк левом hello мы будем toofind все строки, удовлетворяющие условию hello для нашей функции объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="e616a-477">Hello выходного значения должны задаваться с `IUpdatableRow` выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e616a-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="e616a-478">Фактический выход Hello инициируется путем вызова слишком`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e616a-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e616a-479">Ниже приведен пример средства объединения.</span><span class="sxs-lookup"><span data-stu-id="e616a-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="e616a-480">В этом сценарии варианта использования мы будем строить отчета аналитики для hello розничный магазин.</span><span class="sxs-lookup"><span data-stu-id="e616a-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="e616a-481">Задача Hello — toofind продаж всех продуктов стоимостью более 20 000 долларов США и что через веб-сайт hello быстрее, чем через регулярные розничный магазин hello в определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="e616a-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="e616a-482">Вот hello базовый скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="e616a-483">Вы можете сравнить hello логику между обычного СОЕДИНЕНИЯ и функции объединения:</span><span class="sxs-lookup"><span data-stu-id="e616a-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="e616a-484">Определяемые пользователем функции объединения можно вызвать как новый экземпляр объекта применения hello:</span><span class="sxs-lookup"><span data-stu-id="e616a-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="e616a-485">Или с вызовом hello заводского метода оболочки:</span><span class="sxs-lookup"><span data-stu-id="e616a-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="e616a-486">Использование пользовательских средств редукции</span><span class="sxs-lookup"><span data-stu-id="e616a-486">Use user-defined reducers</span></span>

<span data-ttu-id="e616a-487">U-SQL позволяет toowrite reducers пользовательского набора строк в C# с помощью инфраструктуры расширяемости определяемый пользователем оператор hello и реализации интерфейса IReducer.</span><span class="sxs-lookup"><span data-stu-id="e616a-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="e616a-488">Пользовательские редуктора или UDR, можно использовать tooeliminate ненужные строки во время извлечения данных (импорт).</span><span class="sxs-lookup"><span data-stu-id="e616a-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="e616a-489">Его также можно использовать toomanipulate и оценки строк и столбцов.</span><span class="sxs-lookup"><span data-stu-id="e616a-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="e616a-490">На основании логику программирования, он также может определять строк, которые требуется извлечь toobe.</span><span class="sxs-lookup"><span data-stu-id="e616a-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="e616a-491">toodefine класса UDR, нам нужно toocreate `IReducer` интерфейса с помощью необязательного `SqlUserDefinedReducer` атрибута.</span><span class="sxs-lookup"><span data-stu-id="e616a-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="e616a-492">Этот интерфейс класса должен содержать определение для hello `IEnumerable` переопределить интерфейс набора строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="e616a-493">Hello **SqlUserDefinedReducer** атрибут указывает, что hello тип должен быть зарегистрирован как редуктора определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="e616a-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="e616a-494">Этот класс не наследуется.</span><span class="sxs-lookup"><span data-stu-id="e616a-494">This class cannot be inherited.</span></span>
<span data-ttu-id="e616a-495">**SqlUserDefinedReducer** — это необязательный атрибут для определения пользовательских средств редукции.</span><span class="sxs-lookup"><span data-stu-id="e616a-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="e616a-496">Оно использовалось свойство IsRecursive toodefine.</span><span class="sxs-lookup"><span data-stu-id="e616a-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="e616a-497">bool IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="e616a-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="e616a-498">**true** — указывает, что это средство редукции является идемпотентным.</span><span class="sxs-lookup"><span data-stu-id="e616a-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="e616a-499">Основные возможности программирования объектов Hello **входной** и **вывода**.</span><span class="sxs-lookup"><span data-stu-id="e616a-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e616a-500">Hello входной объект — используется tooenumerate входных строк.</span><span class="sxs-lookup"><span data-stu-id="e616a-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="e616a-501">Выходные данные выглядят используется tooset выходные строки в результате уменьшение действия.</span><span class="sxs-lookup"><span data-stu-id="e616a-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="e616a-502">Для перечисления входных строк, мы используем hello `Row.Get` метод.</span><span class="sxs-lookup"><span data-stu-id="e616a-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="e616a-503">Здравствуйте параметр hello `Row.Get` метод — столбец, который передается как часть hello `PRODUCE` класс hello `REDUCE` инструкции базового сценария hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e616a-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="e616a-504">Мы должны toouse hello верный тип данных, здесь также.</span><span class="sxs-lookup"><span data-stu-id="e616a-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="e616a-505">Для выходных данных, используйте hello `output.Set` метод.</span><span class="sxs-lookup"><span data-stu-id="e616a-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="e616a-506">Это важные toounderstand, hello пользовательских редуктора только выходные данные значения, которые определяются с `output.Set` вызова метода.</span><span class="sxs-lookup"><span data-stu-id="e616a-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="e616a-507">выходные данные фактического редуктора Hello инициируется путем вызова `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e616a-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e616a-508">Ниже приведен пример средства редукции.</span><span class="sxs-lookup"><span data-stu-id="e616a-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="e616a-509">В этом сценарии варианта использования редуктора hello пропускает строки с пустым именем.</span><span class="sxs-lookup"><span data-stu-id="e616a-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="e616a-510">Для каждой строки в наборе строк он считывает каждый обязательный столбец, а затем вычисляет hello длина имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e616a-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="e616a-511">Он выводит hello действительного числа строк только в том случае, если длина значения имени пользователя составляет больше 0.</span><span class="sxs-lookup"><span data-stu-id="e616a-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="e616a-512">Ниже представлен основной скрипт U-SQL, который использует пользовательское средство редукции.</span><span class="sxs-lookup"><span data-stu-id="e616a-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```
