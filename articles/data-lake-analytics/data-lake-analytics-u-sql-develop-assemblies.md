---
title: "сборки aaaDevelop U-SQL для задания аналитики Озера данных Azure | Документы Microsoft"
description: "Узнайте, как использовать toobe toodevelop сборки и повторно использовать в аналитике Озера данных задания. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Разработка сборок U-SQL для заданий Azure Data Lake Analytics
Узнайте, как tooturn кода в toobe сборки используется и повторно использоваться в заданиях аналитики Озера данных. 

U-SQL позволяет легко tooadd собственный пользовательский код на языках .net, таких как C#, VB.Net или F #. Можно развернуть собственный toosupport среды выполнения других языков.

Hello простым способом toouse пользовательский код — hello toouse средств Озера данных для возможности кода Visual Studio. Дополнительные сведения см. в статье [Учебник. Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Использование кода программной части имеет несколько недостатков:

- для каждого сценария отправки загружается Hello исходного кода.
- Код программной части не может использоваться совместно с другими заданиями.

tooaddress эти недостатки превратить кода в сборках и зарегистрировать hello сборки toohello аналитики Озера данных каталога.

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012 с установленным Visual C++.
* Пакет SDK Microsoft Azure для .NET (версии 2.5 или выше).  Установите его с помощью установщика веб-платформы hello или установщик Visual Studio
* Учетная запись аналитики озера данных.  См. статью [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).
* Выполните hello [Приступая к работе с студии U-SQL аналитики Озера данных Azure](data-lake-analytics-u-sql-get-started.md) учебника.
* Подключите tooAzure.
* Передача hello источника данных см. в разделе [Приступая к работе с студии U-SQL аналитики Озера данных Azure](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Разработка сборок для U-SQL

**toocreate и отправить задание U-SQL**

1. Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.
2. Разверните **установленные**, **шаблоны**, **Озера данных Azure**, **U-SQL(ADLA)**выберите hello **библиотека классов (для U-SQL Приложение)** шаблона и нажмите кнопку **ОК**.
3. Запишите свой код в файл Class1.cs.  Hello ниже приведен пример кода.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Нажмите кнопку hello **построения** меню, а затем нажмите **построить решение** toocreate hello dll.

## <a name="register-assemblies"></a>Регистрация сборок

Ознакомьтесь с разделом [Использование каталога U-SQL Azure Data Lake Analytics](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Использование сборок hello

В разделе [использование hello данных Озера инструментов Azure для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>См. также
* [Приступая к работе с аналитикой озера данных с помощью PowerShell](data-lake-analytics-get-started-powershell.md)
* [Приступая к работе с hello портал Azure с помощью аналитики Озера данных](data-lake-analytics-get-started-portal.md)
* [Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Использование каталога U-SQL Azure Data Lake Analytics](data-lake-analytics-use-u-sql-catalog.md)
* [Используйте средства Озера данных Azure hello для кода Visual Studio](data-lake-analytics-data-lake-tools-for-vscode.md)
