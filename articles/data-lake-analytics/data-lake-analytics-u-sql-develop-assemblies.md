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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="a76d0-103">Разработка сборок U-SQL для заданий Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a76d0-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="a76d0-104">Узнайте, как tooturn кода в toobe сборки используется и повторно использоваться в заданиях аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="a76d0-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="a76d0-105">U-SQL позволяет легко tooadd собственный пользовательский код на языках .net, таких как C#, VB.Net или F #.</span><span class="sxs-lookup"><span data-stu-id="a76d0-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="a76d0-106">Можно развернуть собственный toosupport среды выполнения других языков.</span><span class="sxs-lookup"><span data-stu-id="a76d0-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="a76d0-107">Hello простым способом toouse пользовательский код — hello toouse средств Озера данных для возможности кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a76d0-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="a76d0-108">Дополнительные сведения см. в статье [Учебник. Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a76d0-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="a76d0-109">Использование кода программной части имеет несколько недостатков:</span><span class="sxs-lookup"><span data-stu-id="a76d0-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="a76d0-110">для каждого сценария отправки загружается Hello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="a76d0-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="a76d0-111">Код программной части не может использоваться совместно с другими заданиями.</span><span class="sxs-lookup"><span data-stu-id="a76d0-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="a76d0-112">tooaddress эти недостатки превратить кода в сборках и зарегистрировать hello сборки toohello аналитики Озера данных каталога.</span><span class="sxs-lookup"><span data-stu-id="a76d0-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a76d0-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a76d0-113">Prerequisites</span></span>
* <span data-ttu-id="a76d0-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012 с установленным Visual C++.</span><span class="sxs-lookup"><span data-stu-id="a76d0-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="a76d0-115">Пакет SDK Microsoft Azure для .NET (версии 2.5 или выше).</span><span class="sxs-lookup"><span data-stu-id="a76d0-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="a76d0-116">Установите его с помощью установщика веб-платформы hello или установщик Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a76d0-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="a76d0-117">Учетная запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="a76d0-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="a76d0-118">См. статью [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a76d0-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="a76d0-119">Выполните hello [Приступая к работе с студии U-SQL аналитики Озера данных Azure](data-lake-analytics-u-sql-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a76d0-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="a76d0-120">Подключите tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a76d0-120">Connect tooAzure.</span></span>
* <span data-ttu-id="a76d0-121">Передача hello источника данных см. в разделе [Приступая к работе с студии U-SQL аналитики Озера данных Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a76d0-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="a76d0-122">Разработка сборок для U-SQL</span><span class="sxs-lookup"><span data-stu-id="a76d0-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="a76d0-123">**toocreate и отправить задание U-SQL**</span><span class="sxs-lookup"><span data-stu-id="a76d0-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="a76d0-124">Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="a76d0-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="a76d0-125">Разверните **установленные**, **шаблоны**, **Озера данных Azure**, **U-SQL(ADLA)**выберите hello **библиотека классов (для U-SQL Приложение)** шаблона и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a76d0-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="a76d0-126">Запишите свой код в файл Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="a76d0-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="a76d0-127">Hello ниже приведен пример кода.</span><span class="sxs-lookup"><span data-stu-id="a76d0-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="a76d0-128">Нажмите кнопку hello **построения** меню, а затем нажмите **построить решение** toocreate hello dll.</span><span class="sxs-lookup"><span data-stu-id="a76d0-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="a76d0-129">Регистрация сборок</span><span class="sxs-lookup"><span data-stu-id="a76d0-129">Register assemblies</span></span>

<span data-ttu-id="a76d0-130">Ознакомьтесь с разделом [Использование каталога U-SQL Azure Data Lake Analytics](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="a76d0-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="a76d0-131">Использование сборок hello</span><span class="sxs-lookup"><span data-stu-id="a76d0-131">Use hello assemblies</span></span>

<span data-ttu-id="a76d0-132">В разделе [использование hello данных Озера инструментов Azure для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="a76d0-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a76d0-133">См. также</span><span class="sxs-lookup"><span data-stu-id="a76d0-133">See also</span></span>
* [<span data-ttu-id="a76d0-134">Приступая к работе с аналитикой озера данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a76d0-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="a76d0-135">Приступая к работе с hello портал Azure с помощью аналитики Озера данных</span><span class="sxs-lookup"><span data-stu-id="a76d0-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a76d0-136">Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL</span><span class="sxs-lookup"><span data-stu-id="a76d0-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="a76d0-137">Использование каталога U-SQL Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a76d0-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="a76d0-138">Используйте средства Озера данных Azure hello для кода Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a76d0-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
