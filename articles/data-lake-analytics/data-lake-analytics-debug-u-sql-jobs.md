---
title: "задания aaaDebug U-SQL | Документы Microsoft"
description: "Узнайте, как toodebug U-SQL не удалось вершин, с помощью Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Отладка определяемого пользователем кода C# для заданий U-SQL, завершившихся сбоем

U-SQL предоставляет модель расширяемости, с помощью C#, поэтому можно написать код tooadd функциональные возможности по работе как пользовательские средства извлечения или редуктора. toolearn более, в разделе [руководство программирования U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). Но, как показывает практика, разработка без ошибок невозможна, а отладка в системах больших данных затруднена, так как многие системы предоставляют достаточно ограниченный набор отладочных сведений о среде, таких как журналы.

Средства Озера данных Azure для Visual Studio предоставляет средство, называемое **не удалось выполнить отладку вершин**, которая позволяет клонировать невыполненного задания с локального компьютера hello облака tooyour для отладки. локальный клон Hello захватывает hello всей облачной среды, включая все входные данные и пользовательского кода.

Hello следующем видео показано, как сбой отладки вершин в средствах Озера данных Azure для Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio требуется hello, следующие два обновления, если они еще не установлены: [Microsoft Visual C++ 2015 распространяемый пакет обновления 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) и [универсальных C времени выполнения для приложений Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Не удалось загрузить вершин toolocal машины

При открытии сбоя задания в средствах Озера данных Azure для Visual Studio, появится желтая панель оповещений с помощью подробных сообщений об ошибках во вкладке "Ошибка" hello.

1. Нажмите кнопку **загрузки** toodownload hello все необходимые ресурсы и входные потоки. Если hello загрузка не завершена, нажмите кнопку **повторите**.

2. Нажмите кнопку **откройте** после завершения загрузки hello toogenerate локальной среде отладки. Будет создан и автоматически открыт новый экземпляр Visual Studio с решением для отладки.

![Azure Data Lake Analytics U-SQL отладка visual studio скачивание вершины](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Задания могут содержать файлы исходного кода или зарегистрированные сборки, и действия по отладке для этих двух типов различаются.

- [Отладка невыполненного задания с кодом программной части](#debug-job-failed-with-code-behind)
- [Отладка невыполненного задания со сборками](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Отладка невыполненного задания с кодом программной части

Если U-SQL происходит сбой операции, а задание hello содержится пользовательский код (обычно называется `Script.usql.cs` в проекте U-SQL), что исходный код импортируется в hello при отладке решения.  Здесь можно использовать hello hello Visual Studio отладки средства (Контрольные значения, переменные, т. д.) tootroubleshoot проблему.

> [!NOTE]
> Перед отладкой, быть убедиться, что toocheck **исключения среды CLR** в параметры исключений окно hello (**Ctrl + Alt + E**).

![Azure Data Lake Analytics U-SQL отладка visual studio настройка](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Нажмите клавишу **F5** toorun hello фонового кода. Он будет выполняться до тех пор, пока не возникнет исключение.

2. Откройте hello `ADLTool_Codebehind.usql.cs` файла и задавать точки останова, затем нажмите клавишу **F5** кода hello toodebug шаг за шагом.

    ![Исключение при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Отладка невыполненного задания со сборками

При использовании зарегистрированных сборок в ваш скрипт U-SQL hello системы не удается получить исходный код hello автоматически. В этом случае следует вручную добавьте hello сборки исходного кода файлы toohello решения.

### <a name="configure-hello-solution"></a>Настройка решения hello

1. Щелкните правой кнопкой мыши **решения «VertexDebug» > Добавить > существующий проект...**  toofind hello сборок исходного кода и добавьте toohello проекта hello отладки решения.

    ![Добавление проекта при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Щелкните правой кнопкой мыши **LocalVertexHost > свойства** в решение и скопируйте hello hello **рабочий каталог** пути.

3. Щелкните правой кнопкой мыши **проект исходного кода сборки > свойства**выберите hello **построения** вкладки в левой части и вставьте путь hello копируются как **выходных данных > выходной путь**.

    ![Настройка пути pdb при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Нажмите клавиши **Ctrl+Alt+E** и проверьте **Исключения среды CLR** в окне параметров исключений.

### <a name="start-debug"></a>Запуск отладки

1. Щелкните правой кнопкой мыши **проект исходного кода сборки > Перестроить** toooutput .pdb файлы toohello `LocalVertexHost` рабочий каталог.

2. Нажмите клавишу **F5** и hello проект будет выполняться, пока она остановлена в результате исключения. Может появиться следующая предупреждение, можно не обращать внимания hello. Он может занять tooa минут tooget toohello отладки экрана.

    ![Azure Data Lake Analytics U-SQL отладка visual studio предупреждение](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Откройте исходный код и задавать точки останова, затем нажмите клавишу **F5** кода hello toodebug шаг за шагом.

Можно также использовать hello hello Visual Studio отладки средства (Контрольные значения, переменные, т. д.) tootroubleshoot проблему.

> [!NOTE]
> Перестройте проект исходного кода hello сборки каждый раз после изменения hello кода обновлена toogenerate PDB-файлы.

После отладки, после успешного выполнения проекта hello hello в окне вывода отображаются hello следующие сообщения:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Успешное завершение отладки U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Повторно отправить задания hello

После завершения отладки повторно отправьте hello невыполненное задание.

1. Для заданий с помощью решений для кода, скопируйте код C# в файл исходного кода hello (обычно `Script.usql.cs`).
2. Для заданий со сборками зарегистрируйте DLL-сборкам hello обновлен в базе данных ADLA:
    1. В обозревателе серверов или Cloud Explorer, разверните hello **ADLA учетной записи > баз данных** узла.
    2. Щелкните правой кнопкой мыши **сборки** и зарегистрировать новый DLL-файл сборки в базе данных ADLA hello: ![отладки Azure аналитика Озера данных U-SQL регистрации сборки](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Повторно отправьте задание.

## <a name="next-steps"></a>Дальнейшие действия

- [Руководство по программированию U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Разработка определяемых пользователем операторов U-SQL для заданий аналитики озера данных Azure](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Учебник. Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
