---
title: "aaaApache Storm топологии с Visual Studio и C# - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Storm топологии на C#. Создайте топологию количество простых word в Visual Studio с помощью средств hello Hadoop для Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="99ced-104">Разрабатывать приложения топологии на C# с помощью средств hello Озера данных для Visual Studio для Apache Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="99ced-105">Узнайте, как toocreate топологии Storm C# с помощью Озера данных Azure hello (Hadoop) tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99ced-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="99ced-106">В этом документе рассматриваются hello процесс создания Storm проекта в Visual Studio, локального тестирования и развертывания tooan Apache Storm на кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="99ced-107">Вы также узнаете, как toocreate гибридной топологии, использующих компоненты C# и Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="99ced-108">Хотя hello в данном пошаговом руководстве зависят от среды разработки Windows с помощью Visual Studio, hello скомпилированный проект может быть отправлено tooeither кластера HDInsight под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="99ced-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="99ced-109">Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="99ced-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="99ced-110">Топология toouse C# в кластере под управлением Linux, необходимо обновить hello пакет Microsoft.SCP.Net.SDK NuGet, используемый в ваш проект tooversion 0.10.0.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="99ced-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="99ced-111">Hello версию пакета hello должно также совпадать hello основной номер версии Storm установлен на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="99ced-112">Версия HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-112">HDInsight version</span></span> | <span data-ttu-id="99ced-113">Версия Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-113">Storm version</span></span> | <span data-ttu-id="99ced-114">Версия SCP.NET</span><span class="sxs-lookup"><span data-stu-id="99ced-114">SCP.NET version</span></span> | <span data-ttu-id="99ced-115">Версия Mono по умолчанию</span><span class="sxs-lookup"><span data-stu-id="99ced-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="99ced-116">3.3</span><span class="sxs-lookup"><span data-stu-id="99ced-116">3.3</span></span> |<span data-ttu-id="99ced-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="99ced-117">0.10.x</span></span> |<span data-ttu-id="99ced-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="99ced-118">0.10.x.x</span></span></br><span data-ttu-id="99ced-119">(только в HDInsight под управлением Windows)</span><span class="sxs-lookup"><span data-stu-id="99ced-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="99ced-120">Нет данных</span><span class="sxs-lookup"><span data-stu-id="99ced-120">NA</span></span> |
| <span data-ttu-id="99ced-121">3.4</span><span class="sxs-lookup"><span data-stu-id="99ced-121">3.4</span></span> | <span data-ttu-id="99ced-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="99ced-122">0.10.0.x</span></span> | <span data-ttu-id="99ced-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="99ced-123">0.10.0.x</span></span> | <span data-ttu-id="99ced-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="99ced-124">3.2.8</span></span> |
| <span data-ttu-id="99ced-125">3,5</span><span class="sxs-lookup"><span data-stu-id="99ced-125">3.5</span></span> | <span data-ttu-id="99ced-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="99ced-126">1.0.2.x</span></span> | <span data-ttu-id="99ced-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="99ced-127">1.0.0.x</span></span> | <span data-ttu-id="99ced-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="99ced-128">4.2.1</span></span> |
| <span data-ttu-id="99ced-129">3.6</span><span class="sxs-lookup"><span data-stu-id="99ced-129">3.6</span></span> | <span data-ttu-id="99ced-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="99ced-130">1.1.0.x</span></span> | <span data-ttu-id="99ced-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="99ced-131">1.0.0.x</span></span> | <span data-ttu-id="99ced-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="99ced-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="99ced-133">C# топологиях для кластеров под управлением Linux необходимо использовать .NET 4.5 и использовать моно toorun hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="99ced-134">Чтобы определить потенциальные проблемы с совместимостью, просмотрите документ о [совместимости Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="99ced-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="99ced-135">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99ced-135">Install Visual Studio</span></span>

<span data-ttu-id="99ced-136">C# топологии с SCP.NET можно разрабатывать с помощью одного из следующих версий Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="99ced-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="99ced-137">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="99ced-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="99ced-138">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="99ced-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="99ced-139">Visual Studio 2015 или [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="99ced-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="99ced-140">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="99ced-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="99ced-141">Установка средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99ced-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="99ced-142">tooinstall Озера данных средства для Visual Studio, выполните действия hello в [приступить к работе с помощью средств Озера данных для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="99ced-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="99ced-143">Установка Java</span><span class="sxs-lookup"><span data-stu-id="99ced-143">Install Java</span></span>

<span data-ttu-id="99ced-144">При отправке топологии Storm из Visual Studio, SCP.NET создает ZIP-файл, содержащий топологии hello и зависимости.</span><span class="sxs-lookup"><span data-stu-id="99ced-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="99ced-145">Java — используется toocreate эти ZIP-файлы, так как он использует формат, который является более совместимым с кластеров на основе Linux.</span><span class="sxs-lookup"><span data-stu-id="99ced-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="99ced-146">Установите hello Java Developer Kit (JDK) 7 или более поздней версии среды разработки.</span><span class="sxs-lookup"><span data-stu-id="99ced-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="99ced-147">Вы можете получить hello Oracle JDK из [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="99ced-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="99ced-148">Вы также можете использовать [другие дистрибутивы Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="99ced-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="99ced-149">Hello `JAVA_HOME` среды переменной должен точки toohello каталог, содержащий Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="99ced-150">Hello `PATH` переменной среды должен включать hello `%JAVA_HOME%\bin` каталога.</span><span class="sxs-lookup"><span data-stu-id="99ced-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="99ced-151">Можно использовать следующие C# консольного приложения tooverify правильность установки Java и hello JDK hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="99ced-152">Шаблоны Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-152">Storm templates</span></span>

<span data-ttu-id="99ced-153">средства Озера данных Hello для Visual Studio предоставляют hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="99ced-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="99ced-154">Тип проекта</span><span class="sxs-lookup"><span data-stu-id="99ced-154">Project type</span></span> | <span data-ttu-id="99ced-155">Что демонстрирует</span><span class="sxs-lookup"><span data-stu-id="99ced-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="99ced-156">Приложение Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-156">Storm Application</span></span> |<span data-ttu-id="99ced-157">Пустой проект топологии Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="99ced-158">Пример модуля записи Storm Azure SQL</span><span class="sxs-lookup"><span data-stu-id="99ced-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="99ced-159">Как toowrite tooAzure базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="99ced-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="99ced-160">Пример модуля чтения Storm Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="99ced-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="99ced-161">Как tooread из базы данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="99ced-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="99ced-162">Пример модуля записи Storm Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="99ced-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="99ced-163">Как toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="99ced-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="99ced-164">Пример модуля чтения концентратора событий Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="99ced-165">Как tooread из концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="99ced-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="99ced-166">Пример модуля записи концентратора событий Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="99ced-167">Как toowrite tooAzure концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="99ced-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="99ced-168">Пример модуля чтения Storm HBase</span><span class="sxs-lookup"><span data-stu-id="99ced-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="99ced-169">Как кластеры tooread из HBase на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="99ced-170">Пример модуля записи Storm HBase</span><span class="sxs-lookup"><span data-stu-id="99ced-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="99ced-171">Как кластеры tooHBase toowrite на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="99ced-172">Пример Storm Hybrid</span><span class="sxs-lookup"><span data-stu-id="99ced-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="99ced-173">Как toouse компонента Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="99ced-174">Пример Storm</span><span class="sxs-lookup"><span data-stu-id="99ced-174">Storm Sample</span></span> |<span data-ttu-id="99ced-175">Базовая топология подсчета слов.</span><span class="sxs-lookup"><span data-stu-id="99ced-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="99ced-176">Не все шаблоны будут работать с HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="99ced-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="99ced-177">Пакеты NuGet, используемые hello шаблоны могут оказаться несовместимыми с моно.</span><span class="sxs-lookup"><span data-stu-id="99ced-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="99ced-178">Проверьте hello [моно совместимости](http://www.mono-project.com/docs/about-mono/compatibility/) документов и использовать hello [анализатор переносимости .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="99ced-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="99ced-179">В hello в данном пошаговом руководстве вы используете hello основные приложения Storm проекта типа toocreate топологии.</span><span class="sxs-lookup"><span data-stu-id="99ced-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="99ced-180">Заметки о шаблонах HBase</span><span class="sxs-lookup"><span data-stu-id="99ced-180">HBase templates notes</span></span>

<span data-ttu-id="99ced-181">Hello HBase чтения и записи шаблоны использовать hello HBase REST API, не hello API-интерфейса Java HBase toocommunicate с HBase на HDInsight кластера.</span><span class="sxs-lookup"><span data-stu-id="99ced-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="99ced-182">Заметки о шаблонах EventHub</span><span class="sxs-lookup"><span data-stu-id="99ced-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99ced-183">Hello EventHub на основе Java spout компонент, входящий в состав hello чтения EventHub шаблона не может работать с Storm в HDInsight версии 3.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="99ced-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="99ced-184">Обновленная версия этого компонента доступна в [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="99ced-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="99ced-185">Пример топологии, которая использует этот компонент и работает со Storm в HDInsight 3.5, см. в [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="99ced-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="99ced-186">Создание топологии на C#</span><span class="sxs-lookup"><span data-stu-id="99ced-186">Create a C# topology</span></span>

1. <span data-ttu-id="99ced-187">Откройте Visual Studio, выберите **Файл** > **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="99ced-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="99ced-188">Из hello **новый проект** окна, разверните **установленные** > **шаблоны**и выберите **Озера данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="99ced-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="99ced-189">Выберите из списка шаблонов hello **Storm приложения**.</span><span class="sxs-lookup"><span data-stu-id="99ced-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="99ced-190">Hello нижней части экрана приветствия, введите **WordCount** как hello имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Снимок экрана: окно "Новый проект"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="99ced-192">После создания проекта hello должно быть hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="99ced-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="99ced-193">**Program.cs**: этот файл определяет hello топологии для вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="99ced-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="99ced-194">Обратите внимание, что по умолчанию создается топология, состоящая из одного объекта spout и одного объекта bolt.</span><span class="sxs-lookup"><span data-stu-id="99ced-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="99ced-195">**Spout.cs**— пример воронки, выдающей случайные числа.</span><span class="sxs-lookup"><span data-stu-id="99ced-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="99ced-196">**Bolt.cs**: пример молнии, отслеживает количество чисел, генерируемой hello spout.</span><span class="sxs-lookup"><span data-stu-id="99ced-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="99ced-197">При создании проекта hello NuGet загрузки последних hello [SCP.NET пакета](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="99ced-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="99ced-198">Реализуйте spout hello</span><span class="sxs-lookup"><span data-stu-id="99ced-198">Implement hello spout</span></span>

1. <span data-ttu-id="99ced-199">Откройте файл **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="99ced-199">Open **Spout.cs**.</span></span> <span data-ttu-id="99ced-200">Spouts, используемые tooread данных в топологии из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="99ced-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="99ced-201">Hello основных компонентов для spout входят:</span><span class="sxs-lookup"><span data-stu-id="99ced-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="99ced-202">**NextTuple**: вызывается Storm при hello spout допускается tooemit новые кортежи.</span><span class="sxs-lookup"><span data-stu-id="99ced-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="99ced-203">**ACK** (только для транзакций топология): обрабатывает подтверждений, инициированное другим компонентам в топологии hello для кортежей, присланные hello spout.</span><span class="sxs-lookup"><span data-stu-id="99ced-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="99ced-204">Подтверждение кортеж позволяет spout hello знать, что он был успешно обработан, нижестоящим компонентам.</span><span class="sxs-lookup"><span data-stu-id="99ced-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="99ced-205">**Сбой** (только для транзакций топология): обрабатывает кортежи, сбой обработки других компонентов в топологии hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="99ced-206">Реализация метода Fail позволяет toore-порождение hello кортежа, чтобы можно было обработать еще раз.</span><span class="sxs-lookup"><span data-stu-id="99ced-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="99ced-207">Замените содержимое hello hello **Spout** класса после текста hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="99ced-208">Это spout случайным образом выдает предложения в топологию hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="99ced-209">Реализовать винты hello</span><span class="sxs-lookup"><span data-stu-id="99ced-209">Implement hello bolts</span></span>

1. <span data-ttu-id="99ced-210">Удалить существующую hello **Bolt.cs** файл из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="99ced-211">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="99ced-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="99ced-212">Выберите из списка hello **молнии Storm**и введите **Splitter.cs** имени hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="99ced-213">Повторите этот процесс toocreate, с именем второго молнии **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="99ced-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="99ced-214">**Splitter.cs** — реализует элемент bolt, который делит предложения на отдельные слова и выдает новый поток слов.</span><span class="sxs-lookup"><span data-stu-id="99ced-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="99ced-215">**Counter.cs**: реализует молнии, который подсчитывает каждого слова и создает новый поток ключевых слов и hello счетчик для каждого слова.</span><span class="sxs-lookup"><span data-stu-id="99ced-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="99ced-216">Эти элементы на чтение и запись toostreams, но можно также использовать toocommunicate молнии с источников, таких как базы данных или службы.</span><span class="sxs-lookup"><span data-stu-id="99ced-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="99ced-217">Откройте файл **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="99ced-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="99ced-218">Он содержит только один метод по умолчанию — **Execute**.</span><span class="sxs-lookup"><span data-stu-id="99ced-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="99ced-219">Hello метод Execute вызывается при молнии hello получает кортеж для обработки.</span><span class="sxs-lookup"><span data-stu-id="99ced-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="99ced-220">Здесь можно считывать и обрабатывать входящие кортежи и создавать исходящие кортежи.</span><span class="sxs-lookup"><span data-stu-id="99ced-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="99ced-221">Замените содержимое hello hello **разделителей** класса hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="99ced-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="99ced-222">Откройте **Counter.cs**и замените содержимое класса hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="99ced-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="99ced-223">Определение топологии hello</span><span class="sxs-lookup"><span data-stu-id="99ced-223">Define hello topology</span></span>

<span data-ttu-id="99ced-224">Spouts и винты выстроены в виде графа, который определяет направление потока данных hello между компонентами.</span><span class="sxs-lookup"><span data-stu-id="99ced-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="99ced-225">Для реализации этой топологии hello graph выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="99ced-225">For this topology, hello graph is as follows:</span></span>

![Схема компонентов](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="99ced-227">Предложения создаются из hello spout и являются распределенные tooinstances молнии разделителей hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="99ced-228">Hello разделителей молнии разбивает hello предложений на слова, являющиеся распределенных toohello счетчика молнии.</span><span class="sxs-lookup"><span data-stu-id="99ced-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="99ced-229">Так как статистика хранится локально в экземпляр счетчика hello, мы хотим убедиться, что конкретные слова потока toohello toomake же экземпляром счетчика молнии.</span><span class="sxs-lookup"><span data-stu-id="99ced-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="99ced-230">Каждое конкретное слово отслеживается только одним экземпляром.</span><span class="sxs-lookup"><span data-stu-id="99ced-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="99ced-231">Поскольку молнии разделителей hello не поддерживает состояние, действительно неважно, какой экземпляр разделителей hello получает какие предложения.</span><span class="sxs-lookup"><span data-stu-id="99ced-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="99ced-232">Откройте файл **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="99ced-232">Open **Program.cs**.</span></span> <span data-ttu-id="99ced-233">Hello важный метод — **GetTopologyBuilder**, которой используется toodefine hello топологии, отправляется tooStorm.</span><span class="sxs-lookup"><span data-stu-id="99ced-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="99ced-234">Замените содержимое hello **GetTopologyBuilder** с hello, следующий код tooimplement hello топологии, описанные выше:</span><span class="sxs-lookup"><span data-stu-id="99ced-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="99ced-235">Отправить hello топологии</span><span class="sxs-lookup"><span data-stu-id="99ced-235">Submit hello topology</span></span>

1. <span data-ttu-id="99ced-236">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="99ced-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99ced-237">При появлении запроса введите учетные данные hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="99ced-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="99ced-238">При наличии более чем одной подписке, войдите в toohello версией, которая содержит ваш ураган в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="99ced-239">Выберите ваш ураган в кластере HDInsight из hello **кластер Storm** раскрывающегося списка, а затем выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="99ced-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="99ced-240">Можно отслеживать при отправке hello успешной с помощью hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="99ced-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="99ced-241">При успешной отправки топологии hello hello **Storm топологии** для hello кластера должны отображаться.</span><span class="sxs-lookup"><span data-stu-id="99ced-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="99ced-242">Выберите hello **WordCount** топологию с hello список tooview сведения о hello под управлением топологии.</span><span class="sxs-lookup"><span data-stu-id="99ced-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99ced-243">**Топологии Storm** можно также просмотреть в **обозревателе сервера**.</span><span class="sxs-lookup"><span data-stu-id="99ced-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="99ced-244">Разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши элемент "Storm" в кластере HDInsight и выберите пункт **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="99ced-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="99ced-245">tooview сведения о компонентах hello в топологии hello, дважды щелкните компонент hello в диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="99ced-246">Из hello **топологии Сводка** щелкните **Kill** toostop hello топологии.</span><span class="sxs-lookup"><span data-stu-id="99ced-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99ced-247">Топологии storm продолжения toorun они будут отключены или удалены hello кластера.</span><span class="sxs-lookup"><span data-stu-id="99ced-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="99ced-248">Транзакционная топология</span><span class="sxs-lookup"><span data-stu-id="99ced-248">Transactional topology</span></span>

<span data-ttu-id="99ced-249">Топология предыдущей Hello является нетранзакционной.</span><span class="sxs-lookup"><span data-stu-id="99ced-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="99ced-250">в топологии hello компоненты Hello не реализуют функциональность tooreplaying сообщений.</span><span class="sxs-lookup"><span data-stu-id="99ced-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="99ced-251">Пример топологии транзакций, создайте проект и выберите **Storm пример** hello тип проекта.</span><span class="sxs-lookup"><span data-stu-id="99ced-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="99ced-252">Реализуйте hello транзакций топологии, после воспроизведения toosupport данных:</span><span class="sxs-lookup"><span data-stu-id="99ced-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="99ced-253">**Кэширование метаданных**: hello spout необходимо хранить метаданные о данных hello, получится, hello данных можно извлечь и повторно создаваться в случае возникновения сбоя.</span><span class="sxs-lookup"><span data-stu-id="99ced-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="99ced-254">Из-за малого данных hello, генерируемой образец hello hello необработанные данные для каждого кортежа хранятся в словаре для воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="99ced-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="99ced-255">**ACK**: каждый молнии в топологии hello можно вызвать `this.ctx.Ack(tuple)` tooacknowledge, что кортеж обработана успешно.</span><span class="sxs-lookup"><span data-stu-id="99ced-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="99ced-256">Здравствуйте, если все элементы имеют запись hello кортежа, `Ack` будет вызван метод hello spout.</span><span class="sxs-lookup"><span data-stu-id="99ced-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="99ced-257">Hello `Ack` метод позволяет hello spout tooremove данные, которые были сохранены для воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="99ced-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="99ced-258">**Сбой**: каждый молнии можно вызвать `this.ctx.Fail(tuple)` tooindicate сбой обработки для кортеж.</span><span class="sxs-lookup"><span data-stu-id="99ced-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="99ced-259">Сбой Hello распространяет toohello `Fail` метод spout hello, где могут быть воспроизведены hello кортежа с помощью кэшированные метаданные.</span><span class="sxs-lookup"><span data-stu-id="99ced-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="99ced-260">**Sequence ID**(Идентификатор последовательности) — при отправке кортежа может быть указан уникальный идентификатор последовательности.</span><span class="sxs-lookup"><span data-stu-id="99ced-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="99ced-261">Это значение определяет hello кортежа для обработки воспроизведения (Ack и сбоя).</span><span class="sxs-lookup"><span data-stu-id="99ced-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="99ced-262">Например, hello spout в hello **Storm образец** проект использует следующие hello при отправке данных:</span><span class="sxs-lookup"><span data-stu-id="99ced-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="99ced-263">Этот код создает кортеж, содержащий поток по умолчанию toohello предложения и значением идентификатора последовательности hello, содержащихся в **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="99ced-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="99ced-264">В этом примере **lastSeqId** увеличивается после каждой отправки кортежа.</span><span class="sxs-lookup"><span data-stu-id="99ced-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="99ced-265">Как показано в hello **Storm пример** проекта, является ли компонент транзакций можно задать во время выполнения, в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99ced-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="99ced-266">Гибридная топология с помощью C# и Java</span><span class="sxs-lookup"><span data-stu-id="99ced-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="99ced-267">Также можно использовать средства Озера данных для Visual Studio toocreate гибридной топологии, где некоторые компоненты являются C#, а другие — Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="99ced-268">Чтобы получить пример гибридной топологии, создайте проект и выберите **Пример гибридного решения Storm**.</span><span class="sxs-lookup"><span data-stu-id="99ced-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="99ced-269">Этот образец демонстрирует следующие основные понятия hello:</span><span class="sxs-lookup"><span data-stu-id="99ced-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="99ced-270">**Компонент spout на Java** и **элемент bolt на C#** — определены в **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="99ced-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="99ced-271">Транзакционная версия определена в **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="99ced-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="99ced-272">**Компонент spout на C#** и **элемент bolt на Java** — определены в **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="99ced-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="99ced-273">Транзакционная версия определена в **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="99ced-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="99ced-274">Эта версия также демонстрирует, как toouse Clojure код из текстового файла, как компонент Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="99ced-275">Топология hello tooswitch, используемый при отправке hello проекта просто переместить hello `[Active(true)]` инструкции toohello топологии требуется toouse, перед его отправкой toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="99ced-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="99ced-276">Все файлы hello Java, которые необходимы предоставляются как часть этого проекта в hello **JavaDependency** папки.</span><span class="sxs-lookup"><span data-stu-id="99ced-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="99ced-277">При создании и отправке гибридной топологии, рассмотрим следующие hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="99ced-278">Необходимо использовать **JavaComponentConstructor** toocreate экземпляр hello класс Java для spout или молнии.</span><span class="sxs-lookup"><span data-stu-id="99ced-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="99ced-279">Следует использовать **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON объекты tooserialize данных в таблицу или из компонентов Java из Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="99ced-280">При отправке hello топологии toohello сервера, необходимо использовать hello **дополнительных конфигураций** hello параметр toospecify **пути к файлам Java**.</span><span class="sxs-lookup"><span data-stu-id="99ced-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="99ced-281">Указанный путь Hello следует hello каталог, содержащий файлы JAR hello, содержащие классы Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="99ced-282">Концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="99ced-282">Azure Event Hubs</span></span>

<span data-ttu-id="99ced-283">Версии SCP.NET 0.9.4.203 появился новый класс и метод специально для работы с spout hello концентратора событий (Java spout, который считывает данные из концентраторов событий).</span><span class="sxs-lookup"><span data-stu-id="99ced-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="99ced-284">При создании топологии, которая использует spout концентратора событий, используйте hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="99ced-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="99ced-285">**EventHubSpoutConfig** класса: создает объект, содержащий конфигурацию hello hello spout компонента.</span><span class="sxs-lookup"><span data-stu-id="99ced-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="99ced-286">**TopologyBuilder.SetEventHubSpout** метод: Добавляет hello концентратора событий spout компонент toohello топологии.</span><span class="sxs-lookup"><span data-stu-id="99ced-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="99ced-287">Необходимо использовать hello **CustomizedInteropJSONSerializer** tooserialize данных, полученных при hello spout.</span><span class="sxs-lookup"><span data-stu-id="99ced-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="99ced-288"><a id="configurationmanager"></a>Использование ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="99ced-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="99ced-289">Не используйте **ConfigurationManager** значения конфигурации tooretrieve винта и spout компонентов.</span><span class="sxs-lookup"><span data-stu-id="99ced-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="99ced-290">Это вызовет исключение пустого указателя.</span><span class="sxs-lookup"><span data-stu-id="99ced-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="99ced-291">Вместо этого hello конфигурацию для проекта передается в топологию Storm hello как пара ключ-значение в контексте топологии hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="99ced-292">Каждый компонент, зависят от значений конфигурации необходимо извлечь их из контекста hello во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="99ced-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="99ced-293">Hello следующий код демонстрирует, как tooretrieve следующих значений:</span><span class="sxs-lookup"><span data-stu-id="99ced-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="99ced-294">При использовании `Get` tooreturn метод экземпляра компонента, необходимо убедиться, передачей обоих hello `Context` и `Dictionary<string, Object>` toohello конструктор параметров.</span><span class="sxs-lookup"><span data-stu-id="99ced-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="99ced-295">Hello следующий пример представляет собой простую `Get` метод, который неправильно передает эти значения:</span><span class="sxs-lookup"><span data-stu-id="99ced-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="99ced-296">Как tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="99ced-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="99ced-297">Последние версии SCP.NET поддерживают обновление пакета через NuGet.</span><span class="sxs-lookup"><span data-stu-id="99ced-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="99ced-298">Если доступно новое обновление, вы получите уведомление об обновлении.</span><span class="sxs-lookup"><span data-stu-id="99ced-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="99ced-299">Проверка toomanually обновления, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="99ced-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="99ced-300">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="99ced-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="99ced-301">Диспетчер пакетов hello, выберите **обновления**.</span><span class="sxs-lookup"><span data-stu-id="99ced-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="99ced-302">Если обновление доступно, оно будет отображено.</span><span class="sxs-lookup"><span data-stu-id="99ced-302">If an update is available, it is listed.</span></span> <span data-ttu-id="99ced-303">Нажмите кнопку **обновление** для hello пакета tooinstall его.</span><span class="sxs-lookup"><span data-stu-id="99ced-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99ced-304">Если проект был создан в более ранней версии, не использующим NuGet SCP.NET, необходимо выполнить следующие шаги tooupdate tooa более новая версия hello:</span><span class="sxs-lookup"><span data-stu-id="99ced-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="99ced-305">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="99ced-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="99ced-306">С помощью hello **поиска** поле, поиск и затем добавить **Microsoft.SCP.Net.SDK** toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="99ced-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="99ced-307">Устранение распространенных неполадок с топологиями</span><span class="sxs-lookup"><span data-stu-id="99ced-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="99ced-308">Исключение пустого указателя</span><span class="sxs-lookup"><span data-stu-id="99ced-308">Null pointer exceptions</span></span>

<span data-ttu-id="99ced-309">При использовании топологии на C# с кластером HDInsight под управлением Linux винта и компоненты, которые используют spout **ConfigurationManager** tooread параметры конфигурации во время выполнения может возвращать исключение указателя null.</span><span class="sxs-lookup"><span data-stu-id="99ced-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="99ced-310">Hello конфигурацию для проекта передается в топологию Storm hello как пара ключ-значение в контексте топологии hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="99ced-311">Его можно извлечь из объекта hello словарь, который передается tooyour компонентов после их инициализации.</span><span class="sxs-lookup"><span data-stu-id="99ced-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="99ced-312">Дополнительные сведения см. в разделе hello [ConfigurationManager](#configurationmanager) раздел этого документа.</span><span class="sxs-lookup"><span data-stu-id="99ced-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="99ced-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="99ced-313">System.TypeLoadException</span></span>

<span data-ttu-id="99ced-314">При использовании топологии на C# с кластером HDInsight под управлением Linux, может возникнуть следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="99ced-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="99ced-315">Эта ошибка возникает при использовании двоичного файла, несовместим с версией .NET, которая поддерживает моно hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="99ced-316">Для кластеров HDInsight под управлением Linux в проекте должны использоваться двоичные файлы, скомпилированные для .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="99ced-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="99ced-317">Локальная проверка топологии</span><span class="sxs-lookup"><span data-stu-id="99ced-317">Test a topology locally</span></span>

<span data-ttu-id="99ced-318">Несмотря на то, что это просто toodeploy кластера tooa топологии, в некоторых случаях может потребоваться tootest топологии локально.</span><span class="sxs-lookup"><span data-stu-id="99ced-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="99ced-319">Используйте следующие шаги toorun hello и протестировать пример топологии hello в этом учебнике локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="99ced-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="99ced-320">Локальное тестирование работает только для базовых топологий на C#.</span><span class="sxs-lookup"><span data-stu-id="99ced-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="99ced-321">Нельзя использовать локальное тестирование для гибридных топологий или топологий, использующих несколько потоков.</span><span class="sxs-lookup"><span data-stu-id="99ced-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="99ced-322">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="99ced-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="99ced-323">В свойствах проекта hello, измените hello **тип вывода** слишком**консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="99ced-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Снимок экрана: свойства проекта с выделенным свойством "Тип выходных данных"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="99ced-325">Запомнить toochange hello **тип вывода** резервное слишком**библиотеки классов** перед развертыванием кластера tooa топологии hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="99ced-326">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **добавить** > **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="99ced-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="99ced-327">Выберите **класса**и введите **LocalTest.cs** имени класса hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="99ced-328">Теперь нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="99ced-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="99ced-329">Откройте **LocalTest.cs**и добавьте следующее hello **с помощью** в начало hello инструкцию:</span><span class="sxs-lookup"><span data-stu-id="99ced-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="99ced-330">Используйте hello следующий код в том, как содержимое hello hello **LocalTest** класса:</span><span class="sxs-lookup"><span data-stu-id="99ced-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="99ced-331">Занять некоторое время tooread через hello комментарии к коду.</span><span class="sxs-lookup"><span data-stu-id="99ced-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="99ced-332">Этот код использует **LocalContext** toorun hello компонентов в среде разработки hello и он будет повторяться hello потока данных между файлами tootext компонентов на локальном диске hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="99ced-333">Откройте **Program.cs**и добавьте следующие toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="99ced-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="99ced-334">Сохранить изменения hello и нажмите кнопку **F5** или выберите **отладки** > **начать отладку** toostart hello проекта.</span><span class="sxs-lookup"><span data-stu-id="99ced-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="99ced-335">Окно консоли должен отображаться, а также состояние журнала в ходе тестов hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="99ced-336">При **завершения тестов** появится, нажмите любое окно hello tooclose ключа.</span><span class="sxs-lookup"><span data-stu-id="99ced-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="99ced-337">Используйте **Проводник** toolocate hello каталог, содержащий проект.</span><span class="sxs-lookup"><span data-stu-id="99ced-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="99ced-338">например **C:\Users\<имя_пользователя>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="99ced-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="99ced-339">В этом каталоге откройте **Bin**, а затем щелкните **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="99ced-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="99ced-340">Вы увидите hello текстовые файлы, которые были созданы при выполнении тестов hello: sentences.txt, counter.txt и splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="99ced-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="99ced-341">Откройте каждый текстовый файл и просматривать данные hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99ced-342">Строковые данные сохраняются в этих файлах как массив значений типа decimal.</span><span class="sxs-lookup"><span data-stu-id="99ced-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="99ced-343">Например, \[[97,103,111]] в hello **splitter.txt** файла — слово hello *и*.</span><span class="sxs-lookup"><span data-stu-id="99ced-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="99ced-344">Быть убедиться, что hello tooset **тип проекта** резервное слишком**библиотеки классов** перед развертыванием tooa Storm в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="99ced-345">Информация о журнале</span><span class="sxs-lookup"><span data-stu-id="99ced-345">Log information</span></span>

<span data-ttu-id="99ced-346">С помощью `Context.Logger`можно легко записывать информацию из компонентов топологии в журнал.</span><span class="sxs-lookup"><span data-stu-id="99ced-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="99ced-347">Например следующие hello создается запись журнала сведений:</span><span class="sxs-lookup"><span data-stu-id="99ced-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="99ced-348">Записанные данные можно просмотреть hello **входа службы Hadoop**, расположенное в **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="99ced-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="99ced-349">Разверните запись hello для вашего ураган в кластере HDInsight, а затем разверните **входа службы Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="99ced-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="99ced-350">Наконец выберите файл tooview hello журнала.</span><span class="sxs-lookup"><span data-stu-id="99ced-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="99ced-351">Hello журналы хранятся в учетной записи хранилища Azure, используемой кластером hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="99ced-352">журналы hello tooview в Visual Studio, необходимо войти в toohello подписки Azure, которой принадлежит учетная запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="99ced-353">Просмотр информации об ошибке</span><span class="sxs-lookup"><span data-stu-id="99ced-353">View error information</span></span>

<span data-ttu-id="99ced-354">tooview ошибки, произошедшие в топологии выполняющегося hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="99ced-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="99ced-355">Из **обозревателя серверов**, щелкните правой кнопкой мыши hello ураган в кластере HDInsight и выберите **Storm представление топологии**.</span><span class="sxs-lookup"><span data-stu-id="99ced-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="99ced-356">Для hello **Spout** и **болтов**, hello **последней ошибки** столбец содержит сведения о последней ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="99ced-357">Выберите hello **Spout идентификатор** или **молнии идентификатор** hello компонента, который содержит ошибку в списке.</span><span class="sxs-lookup"><span data-stu-id="99ced-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="99ced-358">На странице приветствия, ошибка отображается, Дополнительные сведения о указана в hello **ошибки** раздел hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="99ced-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="99ced-359">tooobtain Дополнительные сведения, **порт** из hello **исполнителей** раздел страницы приветствия, toosee hello Storm работника в журнале hello последние несколько минут.</span><span class="sxs-lookup"><span data-stu-id="99ced-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="99ced-360">Ошибки при отправке топологии</span><span class="sxs-lookup"><span data-stu-id="99ced-360">Errors submitting topologies</span></span>

<span data-ttu-id="99ced-361">Если возникают ошибки при отправке tooHDInsight топологии, можно найти журналы для hello серверные компоненты, обрабатывающие топологии отправки в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="99ced-362">Эти журналы, tooretrieve hello используйте следующую команду из командной строки:</span><span class="sxs-lookup"><span data-stu-id="99ced-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="99ced-363">Замените __sshuser__ с hello SSH учетной записи пользователя для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="99ced-364">Замените __clustername__ с именем hello hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="99ced-365">Дополнительные сведения об использовании `scp` и `ssh` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="99ced-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="99ced-366">Отправка может завершиться ошибкой по нескольким причинам:</span><span class="sxs-lookup"><span data-stu-id="99ced-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="99ced-367">JDK не установлен или не находится в пути hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="99ced-368">Необходимые зависимости Java не включаются в отправки hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="99ced-369">Несовместимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="99ced-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="99ced-370">Повторяющиеся имена топологий.</span><span class="sxs-lookup"><span data-stu-id="99ced-370">Duplicate topology names.</span></span>

<span data-ttu-id="99ced-371">Если hello `hdinsight-scpwebapi.out` журнал содержит `FileNotFoundException`, это может быть вызвано hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="99ced-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="99ced-372">Hello JDK не hello пути в среде разработки hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="99ced-373">Убедитесь, что hello JDK установлен в среде разработки hello и что `%JAVA_HOME%/bin` находится в папке hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="99ced-374">Отсутствует зависимость Java.</span><span class="sxs-lookup"><span data-stu-id="99ced-374">You are missing a Java dependency.</span></span> <span data-ttu-id="99ced-375">Убедитесь, что все файлы, необходимые .jar включаются как часть отправки hello.</span><span class="sxs-lookup"><span data-stu-id="99ced-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99ced-376">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99ced-376">Next steps</span></span>

<span data-ttu-id="99ced-377">Пример обработки данных из концентраторов событий см. в статье [Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="99ced-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="99ced-378">Пример топологии C#, которая разбивает поток данных на несколько потоков, см. на странице с [примером C# Storm](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="99ced-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="99ced-379">см. Дополнительные сведения о создании C# топологий, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="99ced-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="99ced-380">Дополнительные способы toowork с HDInsight и дополнительные Storm об образцах, HDInsight см hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="99ced-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="99ced-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="99ced-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="99ced-382">Руководство по программированию для SCP</span><span class="sxs-lookup"><span data-stu-id="99ced-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="99ced-383">**Apache Storm в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="99ced-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="99ced-384">Развертывание и мониторинг топологии с помощью Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99ced-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="99ced-385">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="99ced-386">**Apache Hadoop в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="99ced-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="99ced-387">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="99ced-388">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="99ced-389">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="99ced-390">**Apache HBase в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="99ced-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="99ced-391">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99ced-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
