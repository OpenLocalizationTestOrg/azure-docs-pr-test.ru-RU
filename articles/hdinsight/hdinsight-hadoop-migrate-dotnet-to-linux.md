---
title: "aaaUse .NET с Hadoop MapReduce в HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как toouse приложений .NET для потоковой передачи MapReduce в HDInsight под управлением Linux."
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="a97f7-103">Перенос решений .NET для HDInsight под управлением Windows на основе tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="a97f7-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="a97f7-104">Используйте кластеры HDInsight под управлением Linux [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="a97f7-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="a97f7-105">Моно позволяет toouse компоненты .NET, таких как приложения MapReduce с HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="a97f7-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="a97f7-106">В этом документе сведения способ создания решения toomigrate .NET для toowork кластеры HDInsight под управлением Windows с моно на HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="a97f7-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="a97f7-107">Совместимость Mono с .NET</span><span class="sxs-lookup"><span data-stu-id="a97f7-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="a97f7-108">Mono версии 4.2.1 входит в состав HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="a97f7-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="a97f7-109">Дополнительные сведения о версии hello Mono, входящий в состав HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a97f7-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="a97f7-110">tooinstall моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.</span><span class="sxs-lookup"><span data-stu-id="a97f7-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="a97f7-111">Подробные сведения о совместимости между моно и .NET см. в разделе hello [моно совместимости (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) документа.</span><span class="sxs-lookup"><span data-stu-id="a97f7-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a97f7-112">Hello SCP.NET framework совместим с моно.</span><span class="sxs-lookup"><span data-stu-id="a97f7-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="a97f7-113">Дополнительные сведения об использовании SCP.NET моно см. в разделе [топологии toodevelop C# используйте Visual Studio для Apache Storm на HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a97f7-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="a97f7-114">Автоматический анализ переносимости</span><span class="sxs-lookup"><span data-stu-id="a97f7-114">Automated portability analysis</span></span>

<span data-ttu-id="a97f7-115">Hello [анализатор переносимости .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) может быть toogenerate используется отчет о несовместимости между приложением и Mono.</span><span class="sxs-lookup"><span data-stu-id="a97f7-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="a97f7-116">Используйте следующие шаги tooconfigure hello анализатора toocheck hello приложения для обеспечения переносимости моно:</span><span class="sxs-lookup"><span data-stu-id="a97f7-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="a97f7-117">Установка hello [анализатор переносимости .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="a97f7-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="a97f7-118">Во время установки выберите версию Visual Studio toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a97f7-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="a97f7-119">В Visual Studio 2015 выберите __анализ__ > __параметры анализатор переносимости__и убедитесь, что __4.5__ возврата hello __моно__  раздел.</span><span class="sxs-lookup"><span data-stu-id="a97f7-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![Возврат моно раздел параметров анализатора hello 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="a97f7-121">Выберите __ОК__ toosave hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a97f7-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="a97f7-122">Выберите __Анализ__ > __Analyze Assembly Portability__ (Анализ переносимости сборки).</span><span class="sxs-lookup"><span data-stu-id="a97f7-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="a97f7-123">Выберите hello сборку, содержащую решение, а затем выберите __откройте__ toobegin анализа.</span><span class="sxs-lookup"><span data-stu-id="a97f7-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="a97f7-124">После завершения анализа выберите __Анализ__ > __View analysis reports__ (Просмотр отчетов об анализе).</span><span class="sxs-lookup"><span data-stu-id="a97f7-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="a97f7-125">В __результаты анализа переносимость__выберите __откройте отчет__ tooopen отчета.</span><span class="sxs-lookup"><span data-stu-id="a97f7-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Диалоговое окно результатов анализатора переносимости](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="a97f7-127">Анализатор Hello нельзя перехватить все проблемы с решением.</span><span class="sxs-lookup"><span data-stu-id="a97f7-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="a97f7-128">Например, путь к файлу `c:\temp\file.txt` считается ОК, поскольку моно выполняется в Windows и hello путь является допустимым в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="a97f7-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="a97f7-129">Однако hello путь является недопустимым на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="a97f7-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="a97f7-130">Ручной анализ переносимости</span><span class="sxs-lookup"><span data-stu-id="a97f7-130">Manual portability analysis</span></span>

<span data-ttu-id="a97f7-131">Выполнение аудита вручную с помощью данных hello в hello кода [переносимость приложения (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) документа.</span><span class="sxs-lookup"><span data-stu-id="a97f7-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="a97f7-132">Изменение и выполнение сборки</span><span class="sxs-lookup"><span data-stu-id="a97f7-132">Modify and build</span></span>

<span data-ttu-id="a97f7-133">Продолжайте toobuild toouse Visual Studio .NET решения для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a97f7-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="a97f7-134">Тем не менее необходимо убедиться, что этот проект hello используется настроенный toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="a97f7-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="a97f7-135">Развертывание и тестирование</span><span class="sxs-lookup"><span data-stu-id="a97f7-135">Deploy and test</span></span>

<span data-ttu-id="a97f7-136">После изменения к решению, используя рекомендации hello из hello анализатор переносимости .NET или вручную анализа, необходимо выполнить тестирование с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a97f7-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="a97f7-137">Тестирование решения hello в кластере HDInsight под управлением Linux может раскрыть небольшие проблемы, требующие toobe исправлено.</span><span class="sxs-lookup"><span data-stu-id="a97f7-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="a97f7-138">Мы рекомендуем включить дополнительное ведение журнала в приложении во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="a97f7-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="a97f7-139">Дополнительные сведения о доступе к журналам см. в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="a97f7-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="a97f7-140">Доступ к журналам приложений YARN в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="a97f7-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="a97f7-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a97f7-141">Next steps</span></span>

* [<span data-ttu-id="a97f7-142">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a97f7-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="a97f7-143">Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="a97f7-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="a97f7-144">Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a97f7-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)