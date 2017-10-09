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
# <a name="u-sql-programmability-guide"></a>Руководство по программированию U-SQL

U-SQL — это специальный язык запросов для рабочих нагрузок, обрабатывающих большие данные. Один из компонентов уникальные hello U-SQL — hello сочетание hello SQL-подобного декларативный язык с расширяемостью hello и программирования, предоставляемые языком C#. В этом руководстве мы сосредоточиться на hello расширяемость и Программируемость языка hello U-SQL, который включен в языках C#.

## <a name="requirements"></a>Требования

Скачивание и установка [средств Azure Data Lake для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Начало работы с U-SQL  

Рассмотрим следующий скрипт U-SQL hello.

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

Он определяет набор строк, который называется @a, и создает набор строк, который называется @results, из @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Типы и выражения C# в скрипте U-SQL

Выражение U-SQL — это выражение C# в сочетании с логическими операциями U-SQL, такими как `AND`, `OR`, и `NOT`. Выражения U-SQL можно использовать с инструкциями SELECT, EXTRACT, WHERE, HAVING, GROUP BY и DECLARE.

Например следующий скрипт hello анализирует строку значение DateTime в предложении SELECT hello.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Hello следующий сценарий анализирует строку значение DateTime в операторе DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Использование выражений C# для преобразования типов данных
Hello в следующем примере показано, как преобразование данных даты и времени можно сделать с помощью выражений C#. В данном конкретном случае строковые данные datetime — преобразованный toostandard даты и времени с полуночи прототип времени 00:00:00.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Использование выражений C# для получения текущей даты
toopull сегодняшняя дата, можно использовать следующее выражение C# hello:

```
DateTime.Now.ToString("M/d/yyyy")
```

Ниже приведен пример того, как toouse это выражение в скрипте:

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



## <a name="using-net-assemblies"></a>Использование сборок .NET
Модель расширяемости U-SQL во многом зависит от hello возможность tooadd пользовательский код. В настоящее время U-SQL предоставляет возможности tooadd собственные корпорации Майкрософт. Код на основе .NET (в частности, C#). Однако вы также можете добавить пользовательский код, написанный на других языках .NET, например на VB.NET или F#. 

### <a name="register-a-net-assembly"></a>Регистрация сборки .NET

Используйте tooplace инструкции CREATE ASSEMBLY hello сборкой .NET в базу данных U-SQL. После сборки в базе данных, скрипты U-SQL можно использовать эти сборки с помощью инструкции hello ССЫЛОЧНУЮ СБОРКУ. 

Здравствуйте, как следующий код показывает tooregister сборки:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Здравствуйте, как следующий код показывает tooreference сборки:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Обратитесь к hello [инструкции по регистрации сборки](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) , рассматриваются в этом разделе более подробно.


### <a name="use-assembly-versioning"></a>Использование версий сборок
В настоящее время U-SQL использует hello версии платформы .NET Framework 4.5. Поэтому убедитесь, что ваши собственные совместимы с этой версии среды выполнения hello.

Как упоминалось выше, U-SQL выполняет код в 64-разрядном формате (x64). Поэтому убедитесь, что код является скомпилированных toorun на x64. В противном случае возникнет ошибка Неверный формат hello, показанного выше.

Любой передаваемый в хранилище файл (библиотеки DLL, файлы ресурсов, включая другие среды выполнения, машинные сборки, файлы конфигурации и т. д.) не может быть более 400 МБ. общий размер Hello развернутых ресурсов, либо РАЗВЕРНУТЬ РЕСУРСОВ или с помощью ссылки tooassemblies и их дополнительных файлов, не может превышать 3 ГБ.

И наконец, важно помнить, что в каждой базе данных U-SQL может быть только одна версия любой сборки. Например, если вам требуется версии 7 и версии 8 hello NewtonSoft Json.Net библиотеки, необходимо tooregister их в двух разных базах данных. Кроме того каждый сценарий может ссылаться только на tooone версии данной сборки библиотеки DLL. В этом отношении U-SQL соответствует hello C# сборки управления и управления версиями семантике.


## <a name="use-user-defined-functions-udf"></a>Использование определяемых пользователем функций
U-SQL, определяемые пользователем функции или определяемой пользователем функции, программировании подпрограммы, которые принимают параметры, выполняют действия (например, сложные вычисления) и возвращают hello результат этого действия в качестве значения. Hello возвращаемое значение определяемой пользователем функции может быть только одна скалярная. Основной скрипт U-SQL может вызывать такие функции, как и любую другую скалярную функцию C#.

Мы советуем инициализировать определяемые пользователем функции U-SQL как **общедоступные** (public) и **статические** (static).

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Первый рассмотрим простой пример hello создание определяемой пользователем функции.

В этом сценарии варианта использования мы должны toodetermine hello финансового периода, а именно: hello финансового квартала финансового месяца hello первого входа в систему для конкретного пользователя hello. Hello первый месяц финансового года hello в нашем сценарии — июнь.

финансовый период toocalculate, мы представляем hello следующие функции C#:

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

Она вычисляет финансовый месяц и квартал и возвращает строковое значение. В июне hello первый месяц hello первого финансового квартала, мы используем «Q1:P1». Для июля — "Q1:P2" и т. д.

Это регулярное функции C# Приносим toouse переход в данном проекте U-SQL.

В этом разделе представлен раздел кода hello в этом сценарии:

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

Теперь мы будем toocall этой функции из hello базовый скрипт U-SQL. toodo это, мы иметь полное имя для функции hello, включая пространство имен hello, в этом случае NameSpace.Class.Function(parameter) tooprovide.

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Ниже приведен hello базового сценария фактическое U-SQL:

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

Ниже приведен hello выходной файл hello выполнения скрипта.

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Это простой пример использования встроенной определяемой пользователем функции в U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Сохранение состояния между вызовами определяемой пользователем функции
Объекты программирования C# U-SQL может быть более сложными, используя интерактивность hello кода глобальных переменных. Рассмотрим следующий вариант использования бизнес-сценария hello.

В больших организациях пользователи могут переключаться между разными внутренними приложениями, включая Microsoft Dynamics CRM, Power BI и т. д. Клиентам может потребоваться tooapply анализ телеметрии как пользователи могут переключаться между различными приложениями, при каком использовании hello тенденции являются и т. д. Hello для бизнеса hello предназначена toooptimize использования приложения. Они также может понадобиться toocombine различных приложений или конкретных подпрограммы входа.

tooachieve этой цели, у нас есть toodetermine идентификаторы сеансов и время запаздывания между hello последнего сеанса, которое произошло.

Нам нужна toofind предыдущих вход и затем назначить этот сеансы tooall входа, которые созданный toohello того же приложения. Hello первой проверки является то, что базовый скрипт U-SQL не позволяет нам tooapply вычисления над уже вычисляемых столбцов, с помощью функции LAG. Hello второй задачей является то, что мы tookeep hello конкретного сеанса для всех сеансов в пределах hello же периода времени.

toosolve эту проблему, мы используем глобальной переменной внутри раздела кода: `static public string globalSession;`.

Этой глобальной переменной является весь набор строк применяется toohello во время выполнения наших скрипта.

Ниже приведен раздел кода hello нашей программе U-SQL.

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

В этом примере показано hello глобальная переменная `static public string globalSession;` использовать внутри hello `getStampUserSession` функции и получение повторной инициализации каждого hello время сеанса, изменить параметр.

Базовый скрипт U-SQL Hello выглядит следующим образом:

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

Функция `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` здесь вызывается в процессе hello второй памяти строк вычисления. Она передает hello `UserSessionTimestamp` и возвращает hello значение до `UserSessionTimestamp` изменилось.

выходной файл Hello выглядит следующим образом:

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

В этом примере демонстрируется более сложный вариант использования сценария, в которой используется глобальная переменная в раздел кода, который является набор строк применяется toohello всей памяти.

## <a name="use-user-defined-types-udt"></a>Использование определяемых пользователем типов данных
Определяемые пользователем типы или UDT — это еще одно средство, поддерживающее возможность программирования в U-SQL. Определяемый пользователем тип в U-SQL действует так же, как аналогичный тип в C#. C# является строго типизированным языком, позволяющей hello использовать встроенные и пользовательские типы, определяемые пользователем.

U-SQL не может неявно сериализации или десериализацию произвольный определяемых пользователем типов данных при передаче между вершинами в наборах строк hello определяемого пользователем ТИПА. Это означает, что пользователь hello не tooprovide явного форматирования с помощью интерфейса IFormatter hello. Это обеспечивает U-SQL с hello сериализацию и десериализацию методов для определяемого пользователем ТИПА hello.

> [!NOTE]
> Встроенные средства извлечения и outputters U-SQL в настоящее время невозможно сериализации или десериализацию tooor определяемого пользователем ТИПА данных из файлов даже при использовании набора IFormatter hello. Поэтому при написании файл tooa определяемого пользователем ТИПА данных с hello выходные данные инструкции или считываются с extractor, у вас есть toopass его как строку или массив байтов. Затем вызовите hello сериализации и десериализации кода (то есть метод ToString() hello UDT) явно. Пользовательские средства извлечения и outputters на hello другой стороны, может считывать и записывать определяемых пользователем типов.

Если мы попытаемся toouse определяемого пользователем ТИПА в средство ИЗВЛЕЧЕНИЯ или OUTPUTTER (из предыдущего SELECT), как показано ниже:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Мы получили hello следующая ошибка:

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

toowork с определяемого пользователем ТИПА в outputter, либо имеются tooserialize его toostring с hello метода ToString() или создать пользовательские outputter.

Сейчас определяемые пользователем типы нельзя использовать в инструкции GROUP BY. Если определяемый пользователем тип используется в GROUP BY, возникает следующая ошибка hello:

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

toodefine определяемого пользователем ТИПА, нам нужно:

* Добавьте следующие пространства имен hello:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Добавить `Microsoft.Analytics.Interfaces`, который необходим для интерфейсов hello определяемого пользователем ТИПА. Кроме того `System.IO` необходимые toodefine hello IFormatter интерфейсом.

* Определите определяемый пользователем тип данных с помощью атрибута SqlUserDefinedType.

**SqlUserDefinedType** является определение типа в сборке в виде определяемых пользователем типов (UDT) используется toomark U-SQL. свойства Hello hello атрибута отражают физические характеристики hello hello определяемого пользователем ТИПА. Этот класс не наследуется.

SqlUserDefinedType является обязательным атрибутом для определяемых пользователем типов данных.

Конструктор Hello hello класса:  

* SqlUserDefinedTypeAttribute (модуль форматирования).

* Модуль форматирования: требуется параметр toodefine форматирования определяемого пользователем ТИПА данных — в частности, тип hello hello `IFormatter` интерфейса должен быть передан здесь.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* Типичные определяемого пользователем ТИПА также требует определение интерфейса IFormatter hello, как показано в следующий пример hello:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Hello `IFormatter` интерфейс сериализует и десериализует граф объектов с типом корневого hello \<typeparamref name = «T» >.

\<typeparam name = «T» > Здравствуйте корневом типе для hello объекта графа tooserialize и десериализацию.

* **Выполнить десериализацию**: десериализуются hello данные на hello предоставленный поток и воспроизводит hello граф объектов.

* **Сериализовать**: сериализует объект или граф объектов с hello заданному корневой toohello предоставленный поток.

`MyType`экземпляр: экземпляр типа hello.  
`IColumnWriter`модуль записи или `IColumnReader` чтения: hello базовый поток столбца.  
`ISerializationContext`Контекст: перечисление, которое определяет набор флагов, указывающее hello исходный или целевой контекст для потока hello во время сериализации.

* **Промежуточные**: Указывает, что исходный или целевой контекст hello не материализованного хранилища.

* **Сохраняемости**: Указывает, что исходный или целевой контекст hello материализованного хранилища.

Как и обычный тип C#, определение определяемого пользователем типа данных в U-SQL может переопределять такие операторы, как +/==/!=. Также оно может содержать статические методы. Например, если мы будем toouse данного определяемого пользователем ТИПА как параметра tooa Агрегатная функция MIN U-SQL, у нас есть toodefine < переопределение оператора.

Ранее в этом руководстве мы показали пример для финансового периода код из hello определенную дату в формате hello Qn:Pn (Q1:P10). Следующий пример Hello показано как toodefine пользовательского ввода для значения финансового периода.

Ниже приведен пример раздела кода программной части с определяемым пользователем типом данных и интерфейсом IFormatter.

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

Hello определенный тип включает два числа: квартал и месяц. Здесь определены операторы ==, ! =, >, < и статический метод ToString().

Как упоминалось выше, определяемый пользователем тип данных можно использовать в выражениях SELECT, но нельзя — в средствах OUTPUTTER и EXTRACTOR без настраиваемой сериализации. Она либо содержит toobe сериализованы в виде строки с ToString() или использовать с пользовательской OUTPUTTER и ИЗВЛЕЧЕНИЯ.

Теперь давайте рассмотрим, как можно применять определяемый пользователем тип данных. В разделе кода мы изменили нашей GetFiscalPeriod функция toohello следующее:

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

Как видите, он возвращает значение hello нашей FiscalPeriod типа.

Здесь мы предлагаем примером как toouse, расположенным в базовый скрипт U-SQL. В этом примере представлено несколько способов вызова определяемого пользователем типа данных из скрипта U-SQL.

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

Ниже приведен пример полного раздела кода программной части.

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

## <a name="use-user-defined-aggregates-udagg"></a>Использование определяемых пользователем статистических функций
Определяемые пользователем статистические выражения — это любые функции статистической обработки, не входящие в U-SQL. пример Hello можно статистические tooperform пользовательских математических вычислений, конкатенации строк манипуляций со строками и т. д.

определение определяемой пользователем статистической базового класса Hello выглядит следующим образом:

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

**SqlUserDefinedAggregate** указывает, что тип hello должен быть зарегистрирован как определяемой пользователем статистической функции. Этот класс не наследуется.

Атрибут SqlUserDefinedType является **необязательным** для определяемого пользователем статистического выражения.


Hello базового класса позволяет абстрактные параметры toopass трех: два входных параметров и один — как результат hello. типы данных Hello переменной и должен быть определен во время наследования классов.

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

* **Init** — метод, который вызывается один раз для каждой группы во время вычисления. Он предоставляет процедуры инициализации для каждой группы статистической обработки.  
* **Accumulate** — метод, который выполняется один раз для каждого значения. Он предоставляет основные функции hello для hello статистического алгоритма. Это может быть используется tooaggregate значения с различными типами данных, которые определены во время наследования классов. Он может принимать два параметра разных типов данных.
* **Завершение** выполняется один раз на каждую группу статистической обработки в конце hello обработки toooutput hello результат для каждой группы.

Используйте определение класса hello toodeclare правильные входные данные и типов выходных данных следующим образом:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Первый параметр tooaccumulate
* T2: Первый параметр tooaccumulate
* TResult — возвращаемый тип для метода Terminate.

Например:

```
public class GuidAggregate : IAggregate<string, int, int>
```

или

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Использование определяемых пользователем статистических выражений в U-SQL
toouse определяемой пользователем статистической функции, сначала его определения в коде или сослаться на нее из существующих программирования hello DLL как было сказано ранее.

Затем используйте hello, используя синтаксис:

```
AGG<UDAGG_functionname>(param1,param2)
```

Ниже приведен пример определяемого пользователем статистического выражения.

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

И основной скрипт U-SQL.

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

В этом сценарии варианта использования мы объединения GUID классов для конкретных пользователей hello.

## <a name="use-user-defined-objects-udo"></a>Использование определяемых пользователем объектов
U-SQL позволяет toodefine программирование пользовательских объектов, которые называются определенных пользователем объектов или определяемого пользователем ОПЕРАТОРА.

Hello ниже приведен список определяемого пользователем ОПЕРАТОРА в U-SQL:

* Пользовательские средства извлечения.
    * Извлечение по строкам.
    * Использовать tooimplement извлечения данных из пользовательских структурированных файлов

* Пользовательские средства вывода.
    * Вывод по строкам.
    * Использовать toooutput пользовательских типов данных или настраиваемые форматы файлов

* Пользовательские средства обработки.
    * Получение одной строки и возврат одной строки.
    * Используется tooreduce hello числа столбцов и создают новые столбцы со значениями, которые являются производными от существующего набора столбцов

* Пользовательские средства применения.
    * Принимает одну строку и создает toon строк: 0
    * Использование с инструкциями OUTER и CROSS APPLY.

* Пользовательские средства объединения.
    * Объединяют наборы строк — определяемые пользователем инструкции JOIN.

* Пользовательские средства редукции.
    * Получение n строк и возврат одной строки.
    * Использовать tooreduce hello число строк

Определяемый пользователем ОПЕРАТОР обычно вызывается явным образом в скрипт U-SQL в составе приветствия, следующие инструкции U-SQL:

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> Определяемый пользователем ОПЕРАТОР являются ограниченные tooconsume 0,5 ГБ памяти.  Это ограничение памяти применяется toolocal выполнений.

## <a name="use-user-defined-extractors"></a>Использование пользовательских средств извлечения
U-SQL позволяет tooimport внешних данных с помощью инструкции ИЗВЛЕЧЕНИЯ. Инструкция EXTRACT может использовать встроенные средства извлечения для определяемых пользователем объектов.  

* *Extractors.Text()*: извлекает данные из текстовых файлов с разделителями в разных кодировках.

* *Extractors.Csv()*: извлекает данные из файлов данных с разделителями-запятыми (CSV) в разных кодировках.

* *Extractors.Csv()*: извлекает данные из файлов со значением с разделением знаками табуляции (TSV), в разных кодировках.

Это может быть полезным toodevelop пользовательские извлечения. Это может оказаться полезным во время импорта данных Если мы хотим toodo любой hello следующие задачи:

* Изменить входные данные, разделяя столбцы или изменяя отдельные значения. Hello функциональности ПРОЦЕССОРОВ лучше подходит для объединения столбцов.
* Выполнить синтаксический анализ неструктурированных данных, например веб-страниц или сообщений электронной почты, или частично структурированных данных, например документов XML или JSON.
* Выполнить анализ данных в неподдерживаемых кодировках.

toodefine извлечения, определяемых пользователем, или Включить, нам нужно toocreate `IExtractor` интерфейса. Все входные параметры извлечения toohello, например разделителей столбцов или строк, а также кодирование, должны toobe, определенные в hello конструктор класса hello. Hello `IExtractor` интерфейс также должен содержать определение для hello `IEnumerable<IRow>` переопределить следующим образом:

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

Hello **SqlUserDefinedExtractor** атрибут указывает, что hello тип должен быть зарегистрирован как извлечение, определяемой пользователем. Этот класс не наследуется.

SqlUserDefinedExtractor — это необязательный атрибут для определения пользовательского средства извлечения. Он используется toodefine AtomicFileProcessing свойство для объекта ЛЮЧИТЬ hello.

* bool AtomicFileProcessing.   

* Значение **true** указывает, что это средство извлечения требует атомарные входные файлы (JSON, XML и другие).
* Значение **false** указывает, что это средство извлечения умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).

Hello основные ЛЮЧИТЬ программные объекты не **ввода** и **вывода**. Hello входной объект — входных данных используется tooenumerate как `IUnstructuredReader`. Hello выходной объект — используется tooset выходных данных в результате действия извлечения hello.

Hello входных данных осуществляется с помощью `System.IO.Stream` и `System.IO.StreamReader`.

Перечисление входных столбцов мы сначала разделить hello входного потока с помощью разделителя строки.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Затем еще раз разбиваем входную строку на столбцы:

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset выходные данные, мы используем hello `output.Set` метод.

Очень важно, что toounderstand, hello пользовательские средства извлечения только выводит столбцов и значений, определенных с выводом hello. Вызов метода Set:

```
output.Set<string>(count, part);
```

выходные данные фактического извлечения Hello инициируется путем вызова `yield return output.AsReadOnly();`.

Ниже приведен пример hello извлечения:

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

В этом сценарии варианта использования извлечения hello повторно формирует hello GUID для столбца «guid» и преобразует значения hello случая tooupper столбца «пользователь». Пользовательские средства извлечения могут создавать более сложные результаты, анализируя входные данные и преобразовывая их.

Ниже представлен основной скрипт U-SQL, который использует пользовательское средство извлечения.

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

## <a name="use-user-defined-outputters"></a>Использование пользовательских средств вывода
Определяемые пользователем outputter является другой UDO U-SQL, который позволяет вам tooextend встроенные функциональные возможности U-SQL. Аналогичные toohello извлечения, существует несколько встроенных outputters.

* *Outputters.Text()*: Записывает текстовые файлы с разными кодировками toodelimited данных.
* *Outputters.Csv()*: записывает данные toocomma-запятыми (CSV) файлы различных кодировок.
* *Outputters.Tsv()*: записывает запятыми tootab данных файлов (TSV) различных кодировок.

Пользовательские outputter позволяет toowrite данных в пользовательском формате определенных. Это может быть полезно для hello следующие задачи:

* Запись данных toosemi структурированных и неструктурированных файлов.
* Запись данных в неподдерживаемых кодировках.
* Преобразование выходных данных или добавление пользовательских атрибутов.

toodefine outputter определяемых пользователем, нам нужно toocreate hello `IOutputter` интерфейса.

Ниже приведен базовый hello `IOutputter` реализацию класса:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Все входные параметры toohello outputter, например разделителей столбцов или строк, кодировки и т. д., должны toobe, определенные в hello конструктор класса hello. Hello `IOutputter` интерфейс также должен содержать определение для `void Output` переопределения. атрибут Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` при необходимости можно задать для обработки файла atomic. Дополнительные сведения см. в разделе hello, приведенные ниже сведения.

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

* Метод `Output` вызывается для каждой входной строки. Он возвращает hello `IUnstructuredWriter output` набора строк.
* используется Hello конструктор класса outputter toopass параметры toohello определяемой пользователем.
* `Close`используется toooptionally переопределить состояние дорогих toorelease или определить, когда была сделана последняя строка hello.

**SqlUserDefinedOutputter** атрибут указывает, что hello тип должен быть зарегистрирован как outputter, определяемой пользователем. Этот класс не наследуется.

SqlUserDefinedOutputter — это необязательный атрибут для определения пользовательских средств вывода. Оно использовалось свойство AtomicFileProcessing toodefine hello.

* bool AtomicFileProcessing.   

* **true** — указывает, что это средство вывода требует атомарные выходные файлы (JSON, XML и другие).
* **false** — указывает, что это средство вывода умеет работать с разделенными или распределенными файлами (CSV, SEQ и другие).

Программирование основных объектов Hello **строки** и **вывода**. Hello **строки** объект является используемым tooenumerate выходные данные как `IRow` интерфейса. **Выходные данные** используется tooset вывод данных toohello целевой файл.

Hello выходных данных осуществляется с помощью hello `IRow` интерфейса. Выходные данные передаются построчно.

с помощью метода Get hello интерфейса IRow hello перечисляются Hello отдельных значений:

```
row.Get<string>("column_name")
```

Имена отдельных столбцов можно определить с помощью вызова метода `row.Schema`.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Такой подход позволяет toobuild гибкие outputter для любой схемы метаданных.

Hello выходные данные записываются toofile с помощью `System.IO.StreamWriter`. параметр потока Hello задано слишком`output.BaseStrea` как часть `IUnstructuredWriter output`.

Обратите внимание, что файл toohello буфера данных важно tooflush hello после каждой итерации строк. Кроме того, hello `StreamWriter` объект должен использоваться с hello удаляемого атрибута включен (по умолчанию) и hello **с помощью** ключевое слово:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

В противном случае — после каждой итерации вызывайте явным образом метод Flush(). Это демонстрируется в следующий пример hello.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Установка колонтитулов для пользовательского средства вывода
tooset заголовок, используйте одну итерацию потока выполнения.

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

Сначала Hello кода в hello `if (isHeaderRow)` блок выполняется только один раз.

Для нижнего колонтитула hello, используйте экземпляр ссылок toohello hello `System.IO.Stream` объекта (`output.BaseStream`). Запись hello нижнего колонтитула в hello метод Close() hello `IOutputter` интерфейса.  (Дополнительные сведения см. следующий пример hello.)

Ниже приведен пример пользовательского средства вывода.

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

И основной скрипт U-SQL.

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

Это средство вывода для формата HTML. Оно создает HTML-файл с данными таблицы.

### <a name="call-outputter-from-u-sql-base-script"></a>Вызов средства вывода из основного скрипта U-SQL
toocall пользовательские outputter из hello базовый скрипт U-SQL, новый экземпляр объекта outputter hello hello имеет toobe создан.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid создание экземпляра hello объекта в скрипте базового, можно создать оболочку функции, как показано в примере выше:

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

В этом случае исходного вызова hello выглядит hello следующим образом:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Использование пользовательских средств обработки
Определяемые пользователем процессора или UDP, — это тип определяемого пользователем ОПЕРАТОРА U-SQL, позволяющий tooprocess hello входящих строк, применяя возможности программирования. UDP позволяет toocombine столбцы, изменить значения, а при необходимости, добавить новые столбцы. По сути это помогает tooprocess элементы набора строк tooproduce необходимых данных.

toodefine UDP, нам нужно toocreate `IProcessor` интерфейс с hello `SqlUserDefinedProcessor` атрибут, который является необязательным для протокола UDP.

Этот интерфейс должен содержать определение hello hello `IRow` переопределить интерфейс набора строк, как показано в следующий пример hello:

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

**SqlUserDefinedProcessor** указывает, что hello тип должен быть зарегистрирован как процессор определяемой пользователем. Этот класс не наследуется.

атрибут Hello SqlUserDefinedProcessor **необязательно** для определения UDP.

Основные возможности программирования объектов Hello **входной** и **вывода**. Hello входной объект — используется tooenumerate входные столбцы и выходные данные и tooset выходных данных в результате hello загруженности процессора.

Для перечисления входные столбцы, мы используем hello `input.Get` метод.

```
string column_name = input.Get<string>("column_name");
```

Здравствуйте, параметр `input.Get` метод — столбец, который передается как часть hello `PRODUCE` предложения hello `PROCESS` инструкции базового сценария hello U-SQL. Мы должны toouse hello верный тип данных, здесь.

Для выходных данных, используйте hello `output.Set` метод.

Очень важно toonote этой пользовательской производитель выводит только столбцы и значения, определенные с hello `output.Set` вызова метода.

```
output.Set<string>("mycolumn", mycolumn);
```

выходные данные процессора Hello инициируется путем вызова `return output.AsReadOnly();`.

Ниже приведен пример использования средства обработки.

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

В этом сценарии варианта использования процессора hello создает новый столбец с именем «full_description», объединяя hello существующие столбцы — в этом случае «user» в верхнем регистре, а «des». Он также повторно формирует идентификатор GUID и возвращает hello исходные и новые значения GUID.

Как видно из предыдущего примера hello, можно вызывать методы C# во время `output.Set` вызова метода.

Ниже приведен пример основного скрипта U-SQL, использующего пользовательское средство обработки.

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

## <a name="use-user-defined-appliers"></a>Использование пользовательских средств применения
Объект применения пользовательских U-SQL включает функции tooinvoke пользовательские C# для каждой строки, возвращаемой внешним табличным выражением запроса hello. Hello правый вход оценивается для каждой строки из левого входа hello и объединяются для конечного результата hello hello строки, которые будут созданы. Список столбцов, созданных оператором APPLY hello Hello представляют Привет сочетание hello набор столбцов в hello влево и вправо ввода hello.

Объект применения пользовательских вызывается как часть выражения USQL SELECT hello.

Здравствуйте, типичный вызов toohello определяемого пользователем объекта применения выглядит hello следующим образом:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Дополнительные сведения об использовании средств применения в выражении SELECT см. в статье [U-SQL SELECT, выбрав из CROSS APPLY и OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).

Hello определяемого пользователем объекта применения определение базового класса выглядит следующим образом:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine применения, определяемых пользователем, нам нужно toocreate hello `IApplier` интерфейс с hello [`SqlUserDefinedApplier`] атрибута, который не является обязательным для применения определение определяемой пользователем.

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

* Применить вызывается для каждой строки внешней таблицы hello. Он возвращает hello `IUpdatableRow` вывода набора строк.
* Класс конструктора Hello — применения пользовательских toohello используется toopass параметров.

**SqlUserDefinedApplier** указывает, что hello тип должен быть зарегистрирован как объект применения определяемой пользователем. Этот класс не наследуется.

Атрибут **SqlUserDefinedApplier** является **необязательным** для определения пользовательского средства применения.


Существуют следующие основные возможности программирования объектов Hello.

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Входной набор строк передается в виде ввода `IRow`. Hello выходные строки будут создаваться как `IUpdatableRow` интерфейс вывода.

Имен отдельных столбцов можно определить с помощью вызывающему Привет `IRow` метод схемы.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

tooget hello фактическими значениями данных из входящего hello `IRow`, мы используем метод Get() hello `IRow` интерфейса.

```
mycolumn = row.Get<int>("mycolumn")
```

Или, рекомендуется использовать имя столбца схемы hello:

```
row.Get<int>(row.Schema[0].Name)
```

Hello выходного значения должны задаваться с `IUpdatableRow` выходные данные:

```
output.Set<int>("mycolumn", mycolumn)
```

Это важные toounderstand, пользовательские значения выводить только столбцы и значения, определенные с `output.Set` вызова метода.

Фактический выход Hello инициируется путем вызова `yield return output.AsReadOnly();`.

Конструктор toohello могут передаваться Hello определяемого пользователем объекта применения параметров. Объект применения может возвращать переменное число столбцов, которые должны toobe, определенные во время вызова объекта применения hello в базовый скрипт U-SQL.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Ниже приведен пример применения пользовательских hello.

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

Ниже приведен hello базовый скрипт U-SQL для применения этой определяемой пользователем.

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

В этом сценарии вариантов использования определяемых пользователем зарегистрированную действует как средство синтаксического анализа значения с разделителями запятыми для hello автомобиля парка свойства. строки входной файл Hello выглядеть hello следующим образом:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Это стандартный TSV-файл со значениями с разделением знаками табуляции, в котором столбец свойств содержит такие свойства автомобилей, как производитель, модель и т. д. Эти свойства должны быть проанализированный toohello столбцов таблицы. Hello применения, который предоставляется также позволяет toogenerate динамического количество свойств в hello привести набора строк, на основе параметра hello, которое передается. Вы можете создать либо все свойства, либо определенный набор свойств.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

Объект применения пользовательских Hello можно вызвать как новый экземпляр объекта применения:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Или с вызовом hello заводского метода оболочки:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Использование пользовательских средств объединения
Определяемые пользователем функции объединения или UDC, позволяет toocombine строки из левой и правой наборы строк на основе пользовательской логики. Пользовательское средство объединения используется с выражением COMBINE.

Функции объединения вызывается с hello ОБЪЕДИНЕНИЕ выражение, которое предоставляет hello необходимые сведения об обоих входных наборов строк hello, Группировка столбцов, hello hello ожидаемый результат схемы и Дополнительные сведения.

toocall функции объединения в базовый скрипт U-SQL, мы используем hello, используя синтаксис:

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

Дополнительные сведения см. в [описании выражения COMBINE для U-SQL](https://msdn.microsoft.com/library/azure/mt621339.aspx).

toodefine определяемой пользователем функции объединения, нам нужно toocreate hello `ICombiner` интерфейс с hello [`SqlUserDefinedCombiner`] атрибута, который является необязательным для определения определяемой пользователем функции объединения.

Определение базового класса `ICombiner`.

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

Здравствуйте, пользовательская реализация `ICombiner` интерфейс должен содержать определение hello для `IEnumerable<IRow>` объединить переопределения.

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

Hello **SqlUserDefinedCombiner** атрибут указывает, что тип hello должен быть зарегистрирован как определяемые пользователем функции объединения. Этот класс не наследуется.

**SqlUserDefinedCombiner** — свойство режима используется toodefine hello функции объединения. Он является необязательным атрибутом для определения пользовательских средств объединения.

Режимы CombinerMode

Перечисление CombinerMode может занять hello следующие значения:

* Full (0), потенциально зависит от всех hello входные строки из каждой строки вывода влево и вправо, с hello же значение ключа.

* Left (1), каждая строка выходных данных зависит от одной входной строки слева hello (и потенциально все строки из hello справа с hello же значение ключа).

* Каждая строка выходных данных зависит от одной входной строки из правой hello вправо (2) (и потенциально все строки из левой hello с hello же значение ключа).

* Внутренний (3), каждая строка выходных данных зависит от один входной строки из левой и правой части hello же значение.

Пример: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


Программирование основных объектов Hello являются:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Входные наборы строк передаются в виде левого (**left**) и правого (**right**) интерфейсов типа `IRowset`. Они должны быть перечислены для обработки. Можно выполнять только перечисление каждого интерфейса один раз, поэтому мы tooenumerate и кэшировать его при необходимости.

Для целей кэширования мы можем создать тип структуры памяти List\<T\> как результат выполнения запроса LINQ, в частности создать тип List<`IRow`>. во время перечисления также можно использовать анонимные данные типа Hello.

В разделе [введение tooLINQ запросов (C#)](https://msdn.microsoft.com/library/bb397906.aspx) Дополнительные сведения о запросах LINQ и [IEnumerable\<T\> интерфейс](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) Дополнительные сведения о IEnumerable\<T\> интерфейса.

tooget hello фактическими значениями данных из входящего hello `IRowset`, мы используем метод Get() hello `IRow` интерфейса.

```
mycolumn = row.Get<int>("mycolumn")
```

Имен отдельных столбцов можно определить с помощью вызывающему Привет `IRow` метод схемы.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Или с помощью hello имя столбца схемы:

```
c# row.Get<int>(row.Schema[0].Name)
```

Hello общие перечисления с помощью LINQ выглядит hello следующим образом:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

После перебора обоих наборов строк, мы будем tooloop всех строк. Для каждой строки в наборе строк левом hello мы будем toofind все строки, удовлетворяющие условию hello для нашей функции объединения.

Hello выходного значения должны задаваться с `IUpdatableRow` выходных данных.

```
output.Set<int>("mycolumn", mycolumn)
```

Фактический выход Hello инициируется путем вызова слишком`yield return output.AsReadOnly();`.

Ниже приведен пример средства объединения.

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

В этом сценарии варианта использования мы будем строить отчета аналитики для hello розничный магазин. Задача Hello — toofind продаж всех продуктов стоимостью более 20 000 долларов США и что через веб-сайт hello быстрее, чем через регулярные розничный магазин hello в определенный период времени.

Вот hello базовый скрипт U-SQL. Вы можете сравнить hello логику между обычного СОЕДИНЕНИЯ и функции объединения:

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

Определяемые пользователем функции объединения можно вызвать как новый экземпляр объекта применения hello:

```
USING new MyNameSpace.MyCombiner();
```


Или с вызовом hello заводского метода оболочки:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Использование пользовательских средств редукции

U-SQL позволяет toowrite reducers пользовательского набора строк в C# с помощью инфраструктуры расширяемости определяемый пользователем оператор hello и реализации интерфейса IReducer.

Пользовательские редуктора или UDR, можно использовать tooeliminate ненужные строки во время извлечения данных (импорт). Его также можно использовать toomanipulate и оценки строк и столбцов. На основании логику программирования, он также может определять строк, которые требуется извлечь toobe.

toodefine класса UDR, нам нужно toocreate `IReducer` интерфейса с помощью необязательного `SqlUserDefinedReducer` атрибута.

Этот интерфейс класса должен содержать определение для hello `IEnumerable` переопределить интерфейс набора строк.

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

Hello **SqlUserDefinedReducer** атрибут указывает, что hello тип должен быть зарегистрирован как редуктора определяемой пользователем. Этот класс не наследуется.
**SqlUserDefinedReducer** — это необязательный атрибут для определения пользовательских средств редукции. Оно использовалось свойство IsRecursive toodefine.

* bool IsRecursive.    
* **true** — указывает, что это средство редукции является идемпотентным.

Основные возможности программирования объектов Hello **входной** и **вывода**. Hello входной объект — используется tooenumerate входных строк. Выходные данные выглядят используется tooset выходные строки в результате уменьшение действия.

Для перечисления входных строк, мы используем hello `Row.Get` метод.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Здравствуйте параметр hello `Row.Get` метод — столбец, который передается как часть hello `PRODUCE` класс hello `REDUCE` инструкции базового сценария hello U-SQL. Мы должны toouse hello верный тип данных, здесь также.

Для выходных данных, используйте hello `output.Set` метод.

Это важные toounderstand, hello пользовательских редуктора только выходные данные значения, которые определяются с `output.Set` вызова метода.

```
output.Set<string>("mycolumn", guid);
```

выходные данные фактического редуктора Hello инициируется путем вызова `yield return output.AsReadOnly();`.

Ниже приведен пример средства редукции.

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

В этом сценарии варианта использования редуктора hello пропускает строки с пустым именем. Для каждой строки в наборе строк он считывает каждый обязательный столбец, а затем вычисляет hello длина имени пользователя hello. Он выводит hello действительного числа строк только в том случае, если длина значения имени пользователя составляет больше 0.

Ниже представлен основной скрипт U-SQL, который использует пользовательское средство редукции.

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
