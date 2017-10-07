---
title: "локальный aaaScale U-SQL, запуск и тестирование с помощью пакета SDK U Озера данных Azure SQL | Документы Microsoft"
description: "Узнайте, как toouse SDK U Озера данных Azure SQL tooscale U-SQL заданий локальный запуск и тестирование с помощью командной строки и интерфейсы программирования на локальной рабочей станции."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Масштабирование локального выполнения и тестирования сценариев U-SQL с помощью пакета SDK U-SQL для Azure Data Lake

При разработке скрипт U-SQL, это общие toorun и локально скрипт теста U-SQL перед отправкой toocloud. Для этого сценария Azure Data Lake предоставляет пакет Nuget, который называется пакетом SDK Azure Data Lake для U-SQL, с помощью которого можно легко масштабировать локальное выполнение и тестирование заданий U-SQL. Это также возможно toointegrate U-SQL тестирование с помощью элемента конфигурации (непрерывной интеграции) системы tooautomate hello компиляции и тестирования.

Если вас интересует как toomanually локального запустить и отладить скрипт U-SQL с помощью средства графического пользовательского интерфейса средства Озера данных Azure для Visual Studio можно использовать для этого. Дополнительные сведения см. [здесь](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Установка пакета SDK Azure Data Lake для U-SQL

Вы можете получить hello SDK U Озера данных Azure SQL [здесь](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) на Nuget.org. И перед его использованием необходимо toomake том, что зависимости следующим образом.

### <a name="dependencies"></a>Зависимости

Hello SDK U Озера данных SQL требуется hello следующие зависимости:

- [Microsoft .NET Framework 4.6 или более поздней версии](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 и пакет SDK для Windows 10.0.10240.0 или более поздняя версия (в этой статье он называется пакетом CppSDK). Существует два способа tooget CppSDK:

    - Установка выпуска [Visual Studio Community](https://developer.microsoft.com/downloads/vs-thankyou). Вы получите \Windows Kits\10 папку в папке Program Files hello — например, C:\Program Files (x86) \Windows Kits\10\. Вы также найдете hello версию пакета SDK Windows 10 в \Windows Kits\10\Lib. Если вы не видите эти папки, переустановите Visual Studio и убедиться, что tooselect hello пакета SDK Windows 10 во время установки hello. Если это устанавливается вместе с Visual Studio, hello U-SQL локального компилятор будет искать его автоматически.

    ![Пакет SDK Windows 10 для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Установка [средств Data Lake для Visual Studio](http://aka.ms/adltoolsvs). Можно найти предварительно пакетированных hello файлов Visual C++ и пакет SDK для Windows в C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK. В этом случае локальные компилятора hello U-SQL не удается найти зависимости hello автоматически. Необходимо toospecify hello CppSDK путь для него. Можно скопировать расположение tooanother hello файлы или использовать ее как есть.

## <a name="understand-basic-concepts"></a>Основные понятия

### <a name="data-root"></a>Корневая папка данных

Папка Hello корневой каталог данных является «локальное хранилище» для учетной записи локального вычислений hello. Это учетная запись хранилища Озера данных Azure эквивалентные toohello учетной записи аналитики Озера данных. Переключение tooa папку другой корневой каталог данных является так же, как переключения учетной записи tooa другое хранилище. Если вы хотите tooaccess часто общих данных с папками другой корневой каталог данных, необходимо использовать абсолютные пути в скриптах. Или Создание символических ссылок системных файлов (например, **mklink** в файловой системе NTFS) в папку toopoint hello корневой каталог данных toohello общих данных.

Папка Hello корневой каталог данных используется для:

- Хранение локальных метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.
- Поиск hello входного и выходного пути, которые определяются как относительные пути в U-SQL. Использование относительных путей делает проще toodeploy вашей tooAzure проекты U-SQL.

### <a name="file-path-in-u-sql"></a>Путь к файлу в U-SQL

В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути. относительный путь Hello — toohello относительный путь к папке указанный корневой каталог данных. Рекомендуется, можно использовать «/» как hello toomake разделителя пути скрипты, совместимые со стороны сервера hello. Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты. В этих примерах C:\LocalRunDataRoot — папка hello корневой каталог данных.

|Относительный путь|Абсолютный путь|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Рабочий каталог

При запуске сценария hello U-SQL локально, при компиляции в текущем каталоге выполнения создается рабочий каталог. Кроме выводит toohello компиляции, hello необходимые файлы среды выполнения для локального выполнения будет тени скопированный toothis рабочий каталог. Hello рабочей папки корневой каталог называется «ScopeWorkDir» и hello файлы в рабочий каталог hello, следующим образом:

|Каталог/файл|Каталог/файл|Каталог/файл|Определение|Описание|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Хэш-строка версии среды выполнения|Теневая копия файлов среды выполнения, необходимых для локального выполнения|
| |Script_66AE4909AA0ED06C| |Имя скрипта и хэш-строка пути к скрипту|Выходные данные компиляции и ведение журнала шагов выполнения|
| | |\_script\_.abr|Выходные данные компилятора|Файл Algebra|
| | |\_ScopeCodeGen\_.*|Выходные данные компилятора|Созданный управляемый код|
| | |\_ScopeCodeGenEngine\_.*|Выходные данные компилятора|Созданный собственный код|
| | |referenced assemblies|Ссылка на сборку|Связанные файлы сборок.|
| | |deployed_resources|Развертывание ресурсов|Файлы развертывания ресурсов|
| | |xxxxxxxx.xxx[1..n]\_\*.*|Журнал выполнения|Журнал шагов выполнения|


## <a name="use-hello-sdk-from-hello-command-line"></a>Использовать hello SDK из командной строки hello

### <a name="command-line-interface-of-hello-helper-application"></a>Интерфейс командной строки вспомогательное приложение hello

В разделе SDK directory\build\runtime LocalRunHelper.exe — hello командной строки приложение, которое предоставляет интерфейсы toomost часто используемые hello локального выполнения функции. Обратите внимание, что оба hello команда hello параметры зависят от регистра. tooinvoke его:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Запустите LocalRunHelper.exe без аргументов или с hello **справки** переключения tooshow hello справочной информации:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

В hello справочная информация:

-  **Команда** дает hello имя команды.  
-  **Required Argument** перечисляет обязательные аргументы.  
-  **Optional Argument** перечисляет необязательные аргументы и приводит для них значения по умолчанию.  Необязательные аргументы логическое не принимают параметры, и их отображение указывать tootheir отрицательное значение по умолчанию.

### <a name="return-value-and-logging"></a>Возвращаемое значение и ведение журнала

Возвращает вспомогательное приложение Hello **0** успеха и **-1** сбоя. По умолчанию hello вспомогательный отправляет все сообщения toohello текущей консоли. Однако большинство команд hello поддерживают hello **path_to_log_file - MessageOut** дополнительный аргумент, который перенаправляет hello выводит tooa файла журнала.

### <a name="environment-variable-configuring"></a>Настройка переменной среды

Для локального выполнения U-SQL требуется указать корневую папку данных в качестве локальной учетной записи хранения, а также указать путь к пакету CppSDK для зависимостей. Вы можете оба аргумента набора hello в переменной среды командной строки, и для них.

- Набор hello **SCOPE_CPP_SDK** переменной среды.

    Если Microsoft Visual C++ и пакет SDK для Windows hello, установив Озера Data Tools для Visual Studio, следует проверьте hello следующие папки:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Определите новую переменную среды с именем **SCOPE_CPP_SDK** toopoint toothis каталога. Или скопируйте папку toohello hello другое местоположение и указать **SCOPE_CPP_SDK** , что.

    В переменной среды hello toosetting сложения, можно указать hello **- CppSDK** аргумента при использовании hello командной строки. Этот аргумент переопределяет используемую по умолчанию переменную среды CppSDK.

- Набор hello **LOCALRUN_DATAROOT** переменной среды.

    Определите новую переменную среды с именем **LOCALRUN_DATAROOT** , указывающий корневой каталог данных toohello.

    В переменной среды hello toosetting сложения, можно указать hello **- DataRoot** аргумент с hello путь от корня данных при работе с командной строки. Этот аргумент переопределяет используемую по умолчанию переменную среды, задающую путь к корневой папке данных. Необходимо tooadd этот аргумент командной строки tooevery которого был осуществлен запуск, чтобы переменная среды корневой каталог данных по умолчанию hello для всех операций, можно перезаписать.

### <a name="sdk-command-line-usage-samples"></a>Примеры использования командной строки пакета SDK

#### <a name="compile-and-run"></a>Компиляция и запуск

Hello **запуска** используется команда toocompile hello сценария, а затем выполните скомпилированных результаты. Эта команда принимает все аргументы командной строки, которые доступны для команд **compile** и **execute**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Hello ниже приведены необязательные аргументы для **запуска**:


|Аргумент|Значение по умолчанию|Описание|
|--------|-------------|-----------|
|-CodeBehind|Ложь|сценарий Hello имеет .cs кода программной части|
|-CppSDK| |Каталог CppSDK.|
|-DataRoot| Переменная среды DataRoot|Слишком DataRoot для локального запуска по умолчанию переменная среды «LOCALRUN_DATAROOT»|
|-MessageOut| |Сообщения на консоль tooa файла дампа|
|-Parallel|1|Запустите hello план с hello указан параллелизма|
|-References| |Список путей tooextra ссылочных сборок или файлов данных кода программной части, разделенных «;»|
|-UdoRedirect|Ложь|Создание конфигурации перенаправления сборки Udo.|
|-UseDatabase|master|Toouse базы данных для кода за пределами временную сборку регистрации|
|-Verbose|Ложь|Отображение подробных выходных данных среды выполнения.|
|-WorkDir|Текущий каталог|Задает каталог для работы и выходных данных компилятора.|
|-RunScopeCEP|0|Режим toouse ScopeCEP|
|-ScopeCEPTempPath|temp|Путь к временной toouse для потоковой передачи данных|
|-OptFlags| |Разделенный запятыми список флагов оптимизатора.|


Ниже приведен пример:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Помимо объединения **компиляции** и **выполнение**, можно компилировать и выполнять отдельно hello скомпилированных исполняемых файлов.

#### <a name="compile-a-u-sql-script"></a>Компиляция скрипта U-SQL

Hello **компиляции** команда является tooexecutables сценария используется toocompile U-SQL.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Hello ниже приведены необязательные аргументы для **компиляции**:


|Аргумент|Описание|
|--------|-----------|
| -CodeBehind [значение по умолчанию False]|сценарий Hello имеет .cs кода программной части|
| -CppSDK [значение по умолчанию "]|Каталог CppSDK.|
| -DataRoot [значение по умолчанию: переменная среды DataRoot]|Слишком DataRoot для локального запуска по умолчанию переменная среды «LOCALRUN_DATAROOT»|
| -MessageOut [значение по умолчанию "]|Сообщения на консоль tooa файла дампа|
| -References [значение по умолчанию "]|Список путей tooextra ссылочных сборок или файлов данных кода программной части, разделенных «;»|
| -Shallow [значение по умолчанию False]|Неполная компиляция.|
| -UdoRedirect [значение по умолчанию False]|Создание конфигурации перенаправления сборки Udo.|
| -UseDatabase [значение по умолчанию master]|Toouse базы данных для кода за пределами временную сборку регистрации|
| -WorkDir [значение по умолчанию: текущий каталог]|Задает каталог для работы и выходных данных компилятора.|
| -RunScopeCEP [значение по умолчанию: "0"]|Режим toouse ScopeCEP|
| -ScopeCEPTempPath [значение по умолчанию: "temp"]|Путь к временной toouse для потоковой передачи данных|
| -OptFlags [значение по умолчанию: "]|Разделенный запятыми список флагов оптимизатора.|


Вот несколько примеров использования команды.

Компиляция скрипта U-SQL:

    LocalRunHelper compile -Script d:\test\test1.usql

Скомпилируйте скрипт U-SQL и назначение папки hello корневой каталог данных. Обратите внимание, что это перезапишет hello задать переменную среды.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Компиляция скрипта U-SQL с определенным рабочим каталогом и ссылками на сборку и базу данных:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Выполнение скомпилированного результата

Hello **выполнение** команда является результатов используется tooexecute компиляции.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Hello ниже приведены необязательные аргументы для **выполнение**:

|Аргумент|Описание|
|--------|-----------|
|-DataRoot [значение по умолчанию "]|Корневая папка для обработки метаданных. По умолчанию используется toohello **LOCALRUN_DATAROOT** переменной среды.|
|-MessageOut [значение по умолчанию "]|Выведите сообщения в файл tooa hello консоли.|
|-Parallel [значение по умолчанию 1]|Индикатор toorun hello созданный локального выполнения действия с hello указан уровень параллелизма.|
|-Verbose [значение по умолчанию False]|Индикатор tooshow подробные выходные данные из среды выполнения.|

Пример использования этой команды:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Использование hello SDK с интерфейсами программирования

программные интерфейсы Hello расположены в hello LocalRunHelper.exe. Можно использовать их функции hello toointegrate hello SDK U-SQL и hello tooscale framework теста C# локального тестового скрипт U-SQL. В этой статье я буду использовать hello standard C# модульного тестирования проекта tooshow как toouse эти интерфейсы tootest скрипту U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Шаг 1. Создание проекта модульного теста C# и его настройка

- Создайте проект модульного теста C#, выбрав "Файл" > "Создать" > "Проект" > "Visual C#" > "Тест" > "Проект модульного теста".
- Добавьте LocalRunHelper.exe в качестве ссылки для проекта hello. Hello LocalRunHelper.exe находится в \build\runtime\LocalRunHelper.exe в пакет Nuget.

    ![Добавление ссылки на пакет SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- Пакет SDK U-SQL **только** поддержки x64 среде, убедитесь что tooset целевой платформы сборки как x64. Это можно сделать, выбрав "Свойство проекта" > "Сборка" > "Целевая платформа".

    ![Настройка платформы x64 в проекте для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Убедитесь, что tooset тестовой среды как x64. В Visual Studio это можно сделать, выбрав "Тест" > "Параметры теста" > " 	Архитектура процессора по умолчанию" > "x64".

    ![Настройка тестовой среды x64 для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Убедитесь, что toocopy все файлы зависимостей в рабочем каталоге NugetPackage\build\runtime\ tooproject, которая обычно находится в стадии ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Шаг 2. Создание тестового случая сценария U-SQL

Ниже приведен пример кода hello для теста скрипт U-SQL. Для тестирования, необходимо сценарии tooprepare входных и выходных файлов.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Программные интерфейсы в LocalRunHelper.exe

LocalRunHelper.exe предоставляет программные интерфейсы для локального компиляции U-SQL, запустите hello, интерфейсы hello и т.д., перечислены ниже.

**Конструктор**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|Параметр|Тип|Описание|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|для выходных сообщений задайте toonull toouse консоли|

**Свойства**

|Свойство|Тип|Описание|
|--------|----|-----------|
|AlgebraPath|string|Hello путь к файлу tooalgebra (алгебры файл является одним из результатов компиляции hello)|
|CodeBehindReferences|string|Если скрипт hello дополнительный код программной части ссылки, укажите hello путей, разделенные «;»|
|CppSdkDir|строка|Каталог пакета CppSDK.|
|CurrentDir|строка|Текущий каталог.|
|DataRoot|string|Путь к корневой папке данных.|
|DebuggerMailPath|string|почтовый слот toodebugger путь Hello|
|GenerateUdoRedirect|bool|Если мы хотим загрузки сборки toogenerate перенаправления переопределения конфигурации|
|HasCodeBehind|bool|Если скрипт hello содержит код программной части|
|InputDir|строка|Каталог для входных данных.|
|MessagePath|строка|Путь к файлу дампа сообщений.|
|OutputDir|строка|Каталог для выходных данных.|
|Параллелизм|int|Алгебраические hello toorun параллелизма|
|ParentPid|int|Идентификатор Процесса, на какие hello служба отслеживает tooexit, too0 набор или отрицательным tooignore родителя hello|
|ResultPath|строка|Путь к файлу дампа результатов.|
|RuntimeDir|строка|Каталог среды выполнения.|
|ScriptPath|string|Где toofind hello сценария|
|Shallow|bool|Позволяет задать выполнение неполной компиляции.|
|TempDir|строка|Каталог временных данных|
|UseDataBase|string|Укажите hello toouse базы данных для кода за пределами временную сборку регистрации master по умолчанию|
|WorkDir|строка|Предпочитаемый рабочий каталог.|


**Метод**

|Метод|Описание|Return|Параметр|
|------|-----------|------|---------|
|public bool DoCompile()|Компиляции сценария hello U-SQL|В случае успешного выполнения возвращает True.| |
|public bool DoExec()|Выполнение результата hello компиляции|В случае успешного выполнения возвращает True.| |
|public bool DoRun()|Запустите сценарий hello U-SQL (компиляции + Execute)|В случае успешного выполнения возвращает True.| |
|public bool IsValidRuntimeDir(string path)|Проверьте, является ли заданный путь hello путь допустимое время выполнения|Значение True, если путь допустимый.|Hello путь от каталога среды выполнения|


## <a name="faq-about-common-issue"></a>Часто задаваемые вопросы о распространенных проблемах

### <a name="error-1"></a>Ошибка 1
E_CSC_SYSTEM_INTERNAL: Внутренняя ошибка! Не удалось загрузить файл или сборку "ScopeEngineManaged.dll" либо одну из ее зависимостей. не удалось найти указанный модуль Hello.

Проверьте hello следующее:

- Убедитесь, что используется среда x64. Целевая платформа для построения Hello и hello тестовой среде следует x64 см. в слишком**шаг 1: создание C# модульного тестирования проекта и конфигурация** выше.
- Убедитесь, что вы скопировали все файлы зависимостей в NugetPackage\build\runtime\ tooproject рабочий каталог.


## <a name="next-steps"></a>Дальнейшие действия

* в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).
* сведения диагностики toolog см. в разделе [доступ к журналов диагностики для аналитики Озера данных Azure](data-lake-analytics-diagnostic-logs.md).
* в разделе toosee более сложный запрос, [анализа журналов веб-сайта с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).
* см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md).
* представление выполнения вершин toouse hello, в разделе [hello используйте представление выполнения вершин в средствах Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
