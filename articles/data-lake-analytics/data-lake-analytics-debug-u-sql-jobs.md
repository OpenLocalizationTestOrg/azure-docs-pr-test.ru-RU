---
title: "Отладка пользовательского кода C# для заданий U-SQL Azure Data Lake с ошибками | Документация Майкрософт"
description: "Узнайте, как выполнять отладку вершин U-SQL с ошибками с помощью Средств Azure Data Lake для Visual Studio"
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/31/2017
ms.author: yanacai
ms.openlocfilehash: 739d46753729b70a24dbd3d6e2d78f8513e143e6
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Отладка определяемого пользователем кода C# для заданий U-SQL, завершившихся сбоем

U-SQL поддерживает для C# модель расширяемости. В скриптах U-SQL можно легко вызывать функции C# и выполнять аналитические функции, которые не поддерживаются в декларативных языках, близких к SQL. Дополнительные сведения о расширяемости U-SQL см. в [руководстве по программированию U-SQL](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). 

Как подтверждает практика, отладка может потребоваться для любого кода. Эта задача усложняется, если вы используете распределенное задание, для которого в облаке размещен пользовательский код и доступно лишь ограниченное количество файлов журнала. [Средства Azure Data Lake для Visual Studio](http://aka.ms/adltoolsvs) поддерживают **отладку вершины с ошибками**, которая помогает отлаживать ошибки, возникающие в пользовательском коде. Когда происходит сбой задания U-SQL, служба сохраняет состояние сбоя и позволяет с помощью специального средства скачать облачную среду на момент сбоя, чтобы выполнить отладку на локальном компьютере. В пакете для скачивания содержится вся облачная среда, включая все входные данные и пользовательский код.

Следующее видео демонстрирует использование отладки вершины с ошибками в средствах Azure Data Lake для Visual Studio.

> [!VIDEO https://www.youtube.com/embed/3enkNvprfm4]
>

> [!IMPORTANT]
> Чтобы использовать эту возможность в Visual Studio, необходимо установить следующие два обновления: [Распространяемый компонент Microsoft Visual C++ 2015, обновление 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) и [Универсальная среда выполнения C для Windows](https://www.microsoft.com/download/details.aspx?id=50410).
>

## <a name="download-failed-vertex-to-local-machine"></a>Загрузка на локальный компьютер вершины, в которой произошел сбой

Открывая невыполненное задание в средствах Azure Data Lake для Visual Studio, вы получите оповещение в желтой области оповещений; подробные сведения об ошибке также отобразятся на вкладке "Ошибка".

1. Нажмите кнопку **Скачать** , чтобы скачать все необходимые ресурсы и входные потоки. Нажмите кнопку **Повторить**, если не удалось скачать.

2. Когда загрузка завершится, щелкните **Открыть** для создания локальной среды отладки. Будет создан и автоматически открыт новый экземпляр Visual Studio с решением для отладки.

![Azure Data Lake Analytics U-SQL отладка visual studio скачивание вершины](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

## <a name="configure-the-debugging-environment"></a>Настройка среды отладки

> [!NOTE]
> Перед отладкой обязательно проверьте **исключения среды CLR** в окне параметров исключений (клавиши **CTRL+ALT+E**).

![Azure Data Lake Analytics U-SQL отладка visual studio настройка](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

Новый экземпляр Visual Studio может содержать или не содержать исходный пользовательский код на C#.

1. [Исходный код есть в решении](#source-code-is-included-in-debugging-solution)

2. [Исходный код не удается найти в решении](#source-code-is-not-included-in-debugging-solution)

### <a name="source-code-is-included-in-debugging-solution"></a>Исходный код включен в решение для отладки

Существует два случая, когда исходный код C# сохраняется:

1. пользовательский код определен в файле кода программной части (обычно с именем `Script.usql.cs` в проекте U-SQL);

2. пользовательский код определен в проекте библиотеки классов C# для приложения U-SQL и зарегистрирован как сборка со **сведениями об отладке**.

Если исходный код импортирован в решение, для устранения неполадок можно использовать все средства отладки в Visual Studio (контрольные значения, переменные и т. д.).

1. Нажмите клавишу **F5**, чтобы запустить отладку. Код будет выполняться до тех пор, пока не возникнет исключение.

2. Откройте файл исходного кода и задайте точки останова, затем нажмите клавишу **F5** для пошаговой отладки кода.

    ![Исключение при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

### <a name="source-code-is-not-included-in-debugging-solution"></a>Исходный код не включен в решение для отладки

Если пользовательский код не включен в файл кода программной части или вы не зарегистрировали сборку со **сведениями об отладке**, исходный код не будет автоматически включен в решение для отладки. В этом случае нужно добавить исходный код.

1. Щелкните правой кнопкой мыши **Решение VertexDebug > Добавить > Существующий проект**, чтобы увидеть исходный код сборок и добавить проект в решение для отладки.

    ![Добавление проекта при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Получите путь к папке проекта **FailedVertexDebugHost**. 

3. Щелкните правой кнопкой мыши **Свойства** для добавленного проекта исходного кода сборок. Слева выберите вкладку **Сборка** и вставьте в параметр **Вывод > Выходной путь** скопированный путь, который завершается строкой \bin\debug. Окончательный выходной путь выглядит примерно так: "<DataLakeTemp path>\fd91dd21-776e-4729-a78b-81ad85a4fba6\loiu0t1y.mfo\FailedVertexDebug\FailedVertexDebugHost\bin\Debug\".

    ![Настройка пути pdb при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

Завершив эти настройки, начните отладку с помощью клавиши **F5** и точек останова. Для устранения неполадок можно просто использовать все возможности Visual Studio для отладки (контрольные значения, переменные и т. д.).

> [!NOTE]
> Проект исходного кода сборок необходимо перестраивать после каждого изменения кода, чтобы использовать новые PDB-файлы.

## <a name="resubmit-the-job"></a>Повторная отправка задания

Когда отладка будет завершена, после успешного выполнения проекта в окне вывода отобразится следующее сообщение:

    The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).

![Успешное завершение отладки U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

Чтобы повторно отправить невыполненное задание, выполните следующие действия.

1. Для заданий с кодом программной части скопируйте код C# в файл с кодом программной части (обычно `Script.usql.cs`).

2. Для заданий со сборками щелкните правой кнопкой мыши проект сборки исходного кода в решении для отладки и зарегистрируйте обновленные DLL-файлы сборки в каталог Azure Data Lake.

3. Повторно отправьте задание U-SQL.

## <a name="next-steps"></a>Дальнейшие действия

- [Руководство по программированию U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Разработка определяемых пользователем операторов U-SQL для заданий аналитики озера данных Azure](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake](data-lake-analytics-data-lake-tools-local-run.md)
- [Устранение неполадок, связанных с неправильным повторяющимся заданием](data-lake-analytics-data-lake-tools-debug-recurring-job.md)