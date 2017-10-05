---
title: "Использование .NET с Hadoop MapReduce в HDInsight на платформе Linux в Azure | Документация Майкрософт"
description: "Узнайте, как использовать приложения .NET для потоковой передачи MapReduce в HDInsight под управлением Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="07d8b-103">Перенос решений .NET из HDInsight под управлением Windows в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="07d8b-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="07d8b-104">В кластерах HDInsight под управлением Linux для запуска приложений .NET используется [Mono (https://mono-project.com)](https://mono-project.com).</span><span class="sxs-lookup"><span data-stu-id="07d8b-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="07d8b-105">Mono позволяет использовать компоненты .NET, такие как приложения MapReduce, с HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="07d8b-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="07d8b-106">В этом документе вы узнаете, как перенести решения .NET, созданные для кластеров HDInsight под управлением Windows, на кластеры HDInsight под управлением Linux для работы с Mono.</span><span class="sxs-lookup"><span data-stu-id="07d8b-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="07d8b-107">Совместимость Mono с .NET</span><span class="sxs-lookup"><span data-stu-id="07d8b-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="07d8b-108">Mono версии 4.2.1 входит в состав HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="07d8b-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="07d8b-109">Дополнительные сведения о версии Mono, которая входит в состав HDInsight, см. в разделе [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="07d8b-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="07d8b-110">Чтобы установить определенную версию Mono, см. статью об [установке или обновлении Mono](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="07d8b-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="07d8b-111">Подробные сведения о совместимости Mono и .NET см. в документе [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость Mono).</span><span class="sxs-lookup"><span data-stu-id="07d8b-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07d8b-112">Платформа SCP.NET совместима с Mono.</span><span class="sxs-lookup"><span data-stu-id="07d8b-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="07d8b-113">Дополнительные сведения об использовании SCP.NET с Mono см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="07d8b-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="07d8b-114">Автоматический анализ переносимости</span><span class="sxs-lookup"><span data-stu-id="07d8b-114">Automated portability analysis</span></span>

<span data-ttu-id="07d8b-115">С помощью анализатора [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) можно создать отчет о несовместимости приложения и Mono.</span><span class="sxs-lookup"><span data-stu-id="07d8b-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="07d8b-116">Следуйте приведенным ниже инструкциям по настройке анализатора для проверки приложения на совместимость с Mono.</span><span class="sxs-lookup"><span data-stu-id="07d8b-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="07d8b-117">Установите [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="07d8b-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="07d8b-118">Во время установки выберите используемую версию Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07d8b-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="07d8b-119">В Visual Studio 2015 выберите __Анализ__ > __Portability Analyzer Settings__ (Параметры анализатора переносимости) и убедитесь, что в разделе __Mono__ установлен флажок __4.5__.</span><span class="sxs-lookup"><span data-stu-id="07d8b-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![Установленный флажок "4.5" для Mono в разделе параметров анализатора](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="07d8b-121">Нажмите кнопку __ОК__, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="07d8b-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="07d8b-122">Выберите __Анализ__ > __Analyze Assembly Portability__ (Анализ переносимости сборки).</span><span class="sxs-lookup"><span data-stu-id="07d8b-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="07d8b-123">Выберите сборку, содержащую решение, а затем щелкните __Открыть__, чтобы начать анализ.</span><span class="sxs-lookup"><span data-stu-id="07d8b-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="07d8b-124">После завершения анализа выберите __Анализ__ > __View analysis reports__ (Просмотр отчетов об анализе).</span><span class="sxs-lookup"><span data-stu-id="07d8b-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="07d8b-125">В разделе __Portability Analysis Results__ (Результаты анализа переносимости) щелкните __Открыть отчет__, чтобы открыть отчет.</span><span class="sxs-lookup"><span data-stu-id="07d8b-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Диалоговое окно результатов анализатора переносимости](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="07d8b-127">Анализатор не может выявить все проблемы с решением.</span><span class="sxs-lookup"><span data-stu-id="07d8b-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="07d8b-128">Например, путь к файлу `c:\temp\file.txt` считается корректным, так как Mono работает в среде Windows и в этом контексте путь является допустимым.</span><span class="sxs-lookup"><span data-stu-id="07d8b-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="07d8b-129">Однако такой путь не является допустимым на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="07d8b-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="07d8b-130">Ручной анализ переносимости</span><span class="sxs-lookup"><span data-stu-id="07d8b-130">Manual portability analysis</span></span>

<span data-ttu-id="07d8b-131">Выполните аудит кода вручную, воспользовавшись информацией в документе [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) (Совместимость приложений).</span><span class="sxs-lookup"><span data-stu-id="07d8b-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="07d8b-132">Изменение и выполнение сборки</span><span class="sxs-lookup"><span data-stu-id="07d8b-132">Modify and build</span></span>

<span data-ttu-id="07d8b-133">Можно продолжать использовать Visual Studio для создания решений .NET для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d8b-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="07d8b-134">Однако необходимо обеспечить настройку проекта для использования .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="07d8b-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="07d8b-135">Развертывание и тестирование</span><span class="sxs-lookup"><span data-stu-id="07d8b-135">Deploy and test</span></span>

<span data-ttu-id="07d8b-136">После изменения решения с помощью рекомендаций из результатов .NET Portability Analyzer или ручного анализа необходимо протестировать его работу с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07d8b-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="07d8b-137">Тестирование решения в кластере HDInsight под управлением Linux может выявить малозаметные проблемы, которые необходимо устранить.</span><span class="sxs-lookup"><span data-stu-id="07d8b-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="07d8b-138">Мы рекомендуем включить дополнительное ведение журнала в приложении во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="07d8b-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="07d8b-139">Дополнительные сведения о доступе к журналам см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="07d8b-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="07d8b-140">Доступ к журналам приложений YARN в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="07d8b-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="07d8b-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07d8b-141">Next steps</span></span>

* [<span data-ttu-id="07d8b-142">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="07d8b-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="07d8b-143">Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="07d8b-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="07d8b-144">Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07d8b-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)