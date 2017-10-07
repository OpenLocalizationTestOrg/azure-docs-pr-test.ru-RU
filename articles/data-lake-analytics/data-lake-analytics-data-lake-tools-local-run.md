---
title: "aaaTest и отладки U-SQL заданий с помощью локального запуска и hello U Озера данных Azure SQL пакета SDK | Документы Microsoft"
description: "Узнайте, как toouse средства Озера данных Azure для Visual Studio и SDK U Озера данных Azure SQL tootest hello и отладки U-SQL заданий на локальной рабочей станции."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Тестирование и отладку заданий U-SQL с помощью локального запуска и hello SDK U Озера данных Azure SQL

Так же, как в службе hello Озера данных Azure, можно использовать средства Озера данных Azure для Visual Studio и hello SDK U Озера данных Azure SQL toorun U-SQL заданий на рабочей станции. Оба этих компонента для локального выполнения помогут вам быстрее выполнять тестирование и отладку заданий U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Понимать hello данных корневой папки и путь к файлу hello

Локального запуска и hello SDK U-SQL требуют данных корневую папку. Папка Hello корневой каталог данных является «локальное хранилище» для учетной записи локального вычислений hello. Это учетная запись хранилища Озера данных Azure эквивалентные toohello учетной записи аналитики Озера данных. Переключение tooa папку другой корневой каталог данных является так же, как переключения учетной записи tooa другое хранилище. Если вы хотите tooaccess часто общих данных с папками другой корневой каталог данных, необходимо использовать абсолютные пути в скриптах. Или Создание символических ссылок системных файлов (например, **mklink** в файловой системе NTFS) в папку toopoint hello корневой каталог данных toohello общих данных.

Папка Hello корневой каталог данных используется для:

- Хранение метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.
- Поиск hello входного и выходного пути, которые определяются как относительные пути в U-SQL. Использование относительных путей делает проще toodeploy вашей tooAzure проекты U-SQL.

В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути. относительный путь Hello — toohello относительный путь к папке указанный корневой каталог данных. Рекомендуется, можно использовать «/» как hello toomake разделителя пути скрипты, совместимые со стороны сервера hello. Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты. В этих примерах C:\LocalRunDataRoot — папка hello корневой каталог данных.

|Относительный путь|Абсолютный путь|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Локальное выполнение из Visual Studio

Средства Data Lake для Visual Studio предоставляют возможность локального выполнения U-SQL в Visual Studio. Это позволит вам:

- локально запускать скрипты U-SQL вместе со сборками C#;
- локально выполнять отладку сборок C#;
- создавать, просматривать и удалять каталоги U-SQL (локальные базы данных, сборки, схемы и таблицы) с помощью обозревателя сервера. Также можно также найти hello локального каталога из обозревателя серверов.

    ![Локальный каталог для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Установщик инструментов Озера данных Hello создает C:\LocalRunRoot toobe папки, используемые как папка корневой каталог данных по умолчанию hello. параллелизм локального выполнения Hello по умолчанию — 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure локальном запуске в Visual Studio

1. Откройте Visual Studio.
2. Откройте **обозреватель сервера**.
3. Разверните узлы **Azure** > **Data Lake Analytics**.
4. Нажмите кнопку hello **Озера данных** меню, а затем нажмите **параметры и настройки**.
5. В дереве слева hello разверните **Озера данных Azure**, а затем разверните **Общие**.

    ![Настройка параметров для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Для локального выполнения требуется создать проект U-SQL для Visual Studio. Эта часть выполняется не так, как при запуске скриптов U-SQL в Azure.

### <a name="toorun-a-u-sql-script-locally"></a>скрипт U-SQL toorun локально
1. В Visual Studio откройте нужный проект U-SQL.   
2. В обозревателе решений щелкните правой кнопкой мыши скрипт U-SQL и выберите команду **Submit Script** (Отправить скрипт).
3. Выберите **(Local)** как hello учетной записи в аналитике toorun сценарий локально.
Можно также щелкнуть hello **(Local)** учетную запись на hello верхней части окна «сценарий», а затем нажмите кнопку **отправить** (или используйте Здравствуйте, Ctrl + клавиша F5).

    ![Отправка заданий для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Локальная отладка скриптов и сборок C#

Можно отлаживать C# сборки без отправки и зарегистрировав его tooAzure Служба аналитики Озера данных. Можно установить точки останова в обоих hello файл кода программной части и на которую указывает ссылка проекта C#.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug локальный код в файл кода программной части

1. Установите точки останова в файл с выделенным кодом hello.
2. Нажмите клавишу скрипт hello toodebug F5 локально.

> [!NOTE]
   > Следующая процедура работает только в Visual Studio 2015 Hello. В более старых Visual Studio может потребоваться toomanually добавьте hello PDB-файлы.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>Локальный код toodebug в ссылке проекта C#

1. Создание проекта C# сборки и постройте его toogenerate hello вывода dll.
2. Зарегистрируйте библиотеку dll hello, с помощью инструкции U-SQL:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Установите точки останова в hello кода C#.
4. Нажмите клавишу F5 toodebug hello скрипт при создании ссылок на библиотеки dll hello C# локально.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Использование локального запуска из hello SDK данных Озера U-SQL

Кроме toorunning U-SQL скрипты локально с помощью Visual Studio, можно использовать сценарии U-SQL toorun SDK U Озера данных Azure SQL hello локально с помощью интерфейсов командной строки и программирования. Это позволяет масштабировать сценарии локального тестирования U-SQL.

Узнайте больше о [пакете SDK Azure Data Lake для U-SQL](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Дальнейшие действия

* в разделе toosee более сложный запрос, [анализа журналов веб-сайта с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).
* см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md).
* представление выполнения вершин toouse hello, в разделе [hello используйте представление выполнения вершин в средствах Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
