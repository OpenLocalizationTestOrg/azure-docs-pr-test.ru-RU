---
title: "Разработка сборок U-SQL для заданий Azure Data Lake Analytics | Документация Майкрософт"
description: "Узнайте, как разрабатывать сборки (с возможностью повторного использования) для заданий Data Lake Analytics. "
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
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="3676c-103">Разработка сборок U-SQL для заданий Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3676c-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="3676c-104">Узнайте, как преобразовывать код программной части в сборки (с возможностью повторного использования) для заданий Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3676c-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="3676c-105">U-SQL позволяет с легкостью добавлять собственный пользовательский код на языках .Net, таких как C#, VB.Net или F#.</span><span class="sxs-lookup"><span data-stu-id="3676c-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="3676c-106">Можно даже развернуть собственную среду выполнения для поддержки других языков.</span><span class="sxs-lookup"><span data-stu-id="3676c-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="3676c-107">Проще всего использовать собственный код с помощью средств Data Lake для работы с кодом программной части в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3676c-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="3676c-108">Дополнительные сведения см. в статье [Учебник. Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3676c-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="3676c-109">Использование кода программной части имеет несколько недостатков:</span><span class="sxs-lookup"><span data-stu-id="3676c-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="3676c-110">Исходный код загружается заново при каждой передаче сценария.</span><span class="sxs-lookup"><span data-stu-id="3676c-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="3676c-111">Код программной части не может использоваться совместно с другими заданиями.</span><span class="sxs-lookup"><span data-stu-id="3676c-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="3676c-112">Чтобы устранить эти недостатки, код программной части можно преобразовать в сборки и зарегистрировать их в каталоге Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3676c-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3676c-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3676c-113">Prerequisites</span></span>
* <span data-ttu-id="3676c-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 с обновлением 4 или Visual Studio 2012 с установленным Visual C++.</span><span class="sxs-lookup"><span data-stu-id="3676c-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="3676c-115">Пакет SDK Microsoft Azure для .NET (версии 2.5 или выше).</span><span class="sxs-lookup"><span data-stu-id="3676c-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="3676c-116">Установите эти средства с помощью установщика веб-платформы или установщика Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3676c-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="3676c-117">Учетная запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="3676c-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="3676c-118">См. статью [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3676c-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="3676c-119">Пройдите руководство [Приступая к работе с U-SQL Studio для аналитики озера данных Azure](data-lake-analytics-u-sql-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="3676c-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="3676c-120">Подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="3676c-120">Connect to Azure.</span></span>
* <span data-ttu-id="3676c-121">Загрузите исходные данные. Ознакомьтесь с руководством [Приступая к работе с U-SQL Studio для аналитики озера данных Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3676c-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="3676c-122">Разработка сборок для U-SQL</span><span class="sxs-lookup"><span data-stu-id="3676c-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="3676c-123">**Создание и отправка задания U-SQL**</span><span class="sxs-lookup"><span data-stu-id="3676c-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="3676c-124">В меню **Файл** выберите команду **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="3676c-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="3676c-125">Разверните узел **Установлено**, **Шаблоны**, **Azure Data Lake**, **U-SQL(ADLA)**, выберите шаблон **Class Library (For U-SQL Application)** (Библиотека классов (для приложения U-SQL)) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3676c-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="3676c-126">Запишите свой код в файл Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="3676c-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="3676c-127">Ниже приведен пример кода.</span><span class="sxs-lookup"><span data-stu-id="3676c-127">The following is a code sample.</span></span>

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
4. <span data-ttu-id="3676c-128">Щелкните меню **Сборка** и выберите **Собрать решение**, чтобы создать DLL-файл.</span><span class="sxs-lookup"><span data-stu-id="3676c-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="3676c-129">Регистрация сборок</span><span class="sxs-lookup"><span data-stu-id="3676c-129">Register assemblies</span></span>

<span data-ttu-id="3676c-130">Ознакомьтесь с разделом [Использование каталога U-SQL Azure Data Lake Analytics](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3676c-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="3676c-131">Использование сборок</span><span class="sxs-lookup"><span data-stu-id="3676c-131">Use the assemblies</span></span>

<span data-ttu-id="3676c-132">Ознакомьтесь с разделом [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="3676c-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3676c-133">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="3676c-133">See also</span></span>
* [<span data-ttu-id="3676c-134">Приступая к работе с аналитикой озера данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3676c-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="3676c-135">Приступая к работе с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3676c-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3676c-136">Использование инструментов озера данных для Visual Studio для разработки приложений U-SQL</span><span class="sxs-lookup"><span data-stu-id="3676c-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="3676c-137">Использование каталога U-SQL Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3676c-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="3676c-138">Использование средств Azure Data Lake для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3676c-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)