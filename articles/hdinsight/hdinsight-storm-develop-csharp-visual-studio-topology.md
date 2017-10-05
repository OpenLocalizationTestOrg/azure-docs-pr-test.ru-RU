---
title: "Разработка топологий Apache Storm с помощью Visual Studio и C# — Azure HDInsight | Документы Майкрософт"
description: "Сведения о создании топологий Storm в C#. Создайте простую топологию статистики в Visual Studio с помощью средств Hadoop для Visual Studio."
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="75a0f-104">Разработка топологий для Apache Storm на C# с помощью средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="75a0f-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="75a0f-105">Сведения о создании топологии Storm на языке C# с помощью средств Azure Data Lake (Hadoop) для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75a0f-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="75a0f-106">В этом документе приведены пошаговые инструкции по созданию проекта Storm в Visual Studio, его локальному тестированию и развертыванию в Apache Storm в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="75a0f-107">Вы также узнаете о том, как создавать гибридные топологии, использующие компоненты C# и Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="75a0f-108">Хотя действия, описанные в этой статье, зависят от среды разработки Windows и Visual Studio, скомпилированный проект можно отправить в кластер HDInsight под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="75a0f-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="75a0f-109">Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="75a0f-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="75a0f-110">Чтобы использовать топологию C# с кластером под управлением Linux, обновите пакет NuGet Microsoft.SCP.Net.SDK, использующийся в проекте, до версии 0.10.0.6 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="75a0f-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="75a0f-111">Версия пакета также должна соответствовать основной версии Storm, установленной на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="75a0f-112">Версия HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-112">HDInsight version</span></span> | <span data-ttu-id="75a0f-113">Версия Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-113">Storm version</span></span> | <span data-ttu-id="75a0f-114">Версия SCP.NET</span><span class="sxs-lookup"><span data-stu-id="75a0f-114">SCP.NET version</span></span> | <span data-ttu-id="75a0f-115">Версия Mono по умолчанию</span><span class="sxs-lookup"><span data-stu-id="75a0f-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="75a0f-116">3.3</span><span class="sxs-lookup"><span data-stu-id="75a0f-116">3.3</span></span> |<span data-ttu-id="75a0f-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-117">0.10.x</span></span> |<span data-ttu-id="75a0f-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-118">0.10.x.x</span></span></br><span data-ttu-id="75a0f-119">(только в HDInsight под управлением Windows)</span><span class="sxs-lookup"><span data-stu-id="75a0f-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="75a0f-120">Нет данных</span><span class="sxs-lookup"><span data-stu-id="75a0f-120">NA</span></span> |
| <span data-ttu-id="75a0f-121">3.4</span><span class="sxs-lookup"><span data-stu-id="75a0f-121">3.4</span></span> | <span data-ttu-id="75a0f-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-122">0.10.0.x</span></span> | <span data-ttu-id="75a0f-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-123">0.10.0.x</span></span> | <span data-ttu-id="75a0f-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="75a0f-124">3.2.8</span></span> |
| <span data-ttu-id="75a0f-125">3,5</span><span class="sxs-lookup"><span data-stu-id="75a0f-125">3.5</span></span> | <span data-ttu-id="75a0f-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-126">1.0.2.x</span></span> | <span data-ttu-id="75a0f-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-127">1.0.0.x</span></span> | <span data-ttu-id="75a0f-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="75a0f-128">4.2.1</span></span> |
| <span data-ttu-id="75a0f-129">3.6</span><span class="sxs-lookup"><span data-stu-id="75a0f-129">3.6</span></span> | <span data-ttu-id="75a0f-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-130">1.1.0.x</span></span> | <span data-ttu-id="75a0f-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="75a0f-131">1.0.0.x</span></span> | <span data-ttu-id="75a0f-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="75a0f-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="75a0f-133">Для топологии C# на кластерах под управлением Linux используется .NET 4.5. В кластере HDInsight они запускаются с помощью Mono.</span><span class="sxs-lookup"><span data-stu-id="75a0f-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="75a0f-134">Чтобы определить потенциальные проблемы с совместимостью, просмотрите документ о [совместимости Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="75a0f-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="75a0f-135">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="75a0f-135">Install Visual Studio</span></span>

<span data-ttu-id="75a0f-136">Для разработки топологий C# с помощью SCP.NET можно использовать одну из следующих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="75a0f-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="75a0f-137">Visual Studio 2012 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="75a0f-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="75a0f-138">Visual Studio 2013 с [обновлением 4](http://www.microsoft.com/download/details.aspx?id=44921) или [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="75a0f-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="75a0f-139">Visual Studio 2015 или [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="75a0f-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="75a0f-140">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="75a0f-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="75a0f-141">Установка средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="75a0f-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="75a0f-142">Инструкции по установке средств Data Lake для Visual Studio см. в статье [Подключение к Azure HDInsight и выполнение запросов Hive с помощью средств Data Lake для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="75a0f-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="75a0f-143">Установка Java</span><span class="sxs-lookup"><span data-stu-id="75a0f-143">Install Java</span></span>

<span data-ttu-id="75a0f-144">При отправке топологии Storm из Visual Studio SCP.NET создает ZIP-файл, содержащий топологию и зависимости.</span><span class="sxs-lookup"><span data-stu-id="75a0f-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="75a0f-145">Эти ZIP-файлы создаются с помощью Java, так как при этом используется формат, который более совместим с кластерами под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="75a0f-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="75a0f-146">Установите Java Developer Kit (JDK) 7 или более поздней версии в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="75a0f-147">Получить пакет Oracle JDK можно на сайте [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="75a0f-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="75a0f-148">Вы также можете использовать [другие дистрибутивы Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="75a0f-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="75a0f-149">Переменная среды `JAVA_HOME` должна указывать на каталог, содержащий Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="75a0f-150">Переменная среды `PATH` должна включать в себя каталог `%JAVA_HOME%\bin`.</span><span class="sxs-lookup"><span data-stu-id="75a0f-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="75a0f-151">Для проверки правильности установки Java и пакета JDK можно использовать следующее консольное приложение C#:</span><span class="sxs-lookup"><span data-stu-id="75a0f-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="75a0f-152">Шаблоны Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-152">Storm templates</span></span>

<span data-ttu-id="75a0f-153">Средства Data Lake для Visual Studio предоставляют следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="75a0f-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="75a0f-154">Тип проекта</span><span class="sxs-lookup"><span data-stu-id="75a0f-154">Project type</span></span> | <span data-ttu-id="75a0f-155">Что демонстрирует</span><span class="sxs-lookup"><span data-stu-id="75a0f-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="75a0f-156">Приложение Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-156">Storm Application</span></span> |<span data-ttu-id="75a0f-157">Пустой проект топологии Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="75a0f-158">Пример модуля записи Storm Azure SQL</span><span class="sxs-lookup"><span data-stu-id="75a0f-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="75a0f-159">Запись в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0f-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="75a0f-160">Пример модуля чтения Storm Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="75a0f-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="75a0f-161">Чтение из базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="75a0f-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="75a0f-162">Пример модуля записи Storm Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="75a0f-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="75a0f-163">Запись в базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="75a0f-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="75a0f-164">Пример модуля чтения концентратора событий Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="75a0f-165">Чтение из концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0f-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="75a0f-166">Пример модуля записи концентратора событий Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="75a0f-167">Запись в концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0f-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="75a0f-168">Пример модуля чтения Storm HBase</span><span class="sxs-lookup"><span data-stu-id="75a0f-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="75a0f-169">Чтение из HBase в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="75a0f-170">Пример модуля записи Storm HBase</span><span class="sxs-lookup"><span data-stu-id="75a0f-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="75a0f-171">Запись в HBase в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="75a0f-172">Пример Storm Hybrid</span><span class="sxs-lookup"><span data-stu-id="75a0f-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="75a0f-173">Использование компонентов Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-173">How to use a Java component.</span></span> |
| <span data-ttu-id="75a0f-174">Пример Storm</span><span class="sxs-lookup"><span data-stu-id="75a0f-174">Storm Sample</span></span> |<span data-ttu-id="75a0f-175">Базовая топология подсчета слов.</span><span class="sxs-lookup"><span data-stu-id="75a0f-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="75a0f-176">Не все шаблоны будут работать с HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="75a0f-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="75a0f-177">Пакеты NuGet, используемые в шаблонах, могут оказаться несовместимыми с Mono.</span><span class="sxs-lookup"><span data-stu-id="75a0f-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="75a0f-178">Проверьте документацию по [совместимости с Mono](http://www.mono-project.com/docs/about-mono/compatibility/) и используйте [анализатор переносимости .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis), чтобы определить возможные проблемы.</span><span class="sxs-lookup"><span data-stu-id="75a0f-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="75a0f-179">На данном этапе в этом документе используется базовый тип проекта приложения Storm для создания топологии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="75a0f-180">Заметки о шаблонах HBase</span><span class="sxs-lookup"><span data-stu-id="75a0f-180">HBase templates notes</span></span>

<span data-ttu-id="75a0f-181">Для взаимодействия с HBase в кластере HDInsight шаблоны модулей чтения и записи HBase используют REST API HBase, а не API Java HBase.</span><span class="sxs-lookup"><span data-stu-id="75a0f-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="75a0f-182">Заметки о шаблонах EventHub</span><span class="sxs-lookup"><span data-stu-id="75a0f-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75a0f-183">Компонент spout EventHub на основе Java, входящий в состав шаблона EventHub Reader, не работает со Storm в HDInsight версии 3.5 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="75a0f-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="75a0f-184">Обновленная версия этого компонента доступна в [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="75a0f-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="75a0f-185">Пример топологии, которая использует этот компонент и работает со Storm в HDInsight 3.5, см. в [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="75a0f-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="75a0f-186">Создание топологии на C#</span><span class="sxs-lookup"><span data-stu-id="75a0f-186">Create a C# topology</span></span>

1. <span data-ttu-id="75a0f-187">Откройте Visual Studio, выберите **Файл** > **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="75a0f-188">В окне **Новый проект** разверните **Установленные** > **Шаблоны** и выберите **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="75a0f-189">В списке шаблонов выберите **Приложение Storm**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="75a0f-190">В нижней части диалогового окна введите имя приложения **WordCount** .</span><span class="sxs-lookup"><span data-stu-id="75a0f-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Снимок экрана: окно "Новый проект"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="75a0f-192">После создания проекта у вас должны быть следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="75a0f-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="75a0f-193">**Program.cs** — определяет топологию для проекта.</span><span class="sxs-lookup"><span data-stu-id="75a0f-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="75a0f-194">Обратите внимание, что по умолчанию создается топология, состоящая из одного объекта spout и одного объекта bolt.</span><span class="sxs-lookup"><span data-stu-id="75a0f-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="75a0f-195">**Spout.cs**— пример воронки, выдающей случайные числа.</span><span class="sxs-lookup"><span data-stu-id="75a0f-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="75a0f-196">**Bolt.cs**— пример сита, которое подсчитывает числа, созданные воронкой.</span><span class="sxs-lookup"><span data-stu-id="75a0f-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="75a0f-197">При создании проекта NuGet скачивает последнюю версию [пакета SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="75a0f-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="75a0f-198">Реализация воронки</span><span class="sxs-lookup"><span data-stu-id="75a0f-198">Implement the spout</span></span>

1. <span data-ttu-id="75a0f-199">Откройте файл **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-199">Open **Spout.cs**.</span></span> <span data-ttu-id="75a0f-200">Воронки используются для считывания данных в топологии из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="75a0f-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="75a0f-201">Ниже перечислены основные компоненты воронки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="75a0f-202">**NextTuple**(Следующий кортеж) — вызывается Storm, когда воронке разрешено создавать новые кортежи.</span><span class="sxs-lookup"><span data-stu-id="75a0f-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="75a0f-203">**Ack** (Подтверждение, только для транзакционной топологии) — обрабатывает подтверждения, инициированные другими компонентами топологии для кортежей, отправленных из этой воронки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="75a0f-204">Подтверждение кортежа позволяет воронке определить, что он был успешно обработан нижестоящими компонентами.</span><span class="sxs-lookup"><span data-stu-id="75a0f-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="75a0f-205">**Fail** (Сбой, только для транзакционной топологии) — обрабатывает кортежи, обработка которых другими компонентами топологии завершилась сбоем.</span><span class="sxs-lookup"><span data-stu-id="75a0f-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="75a0f-206">Реализация метода Fail дает возможность повторно создать кортеж для повторной обработки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="75a0f-207">Замените содержимое класса **Spout** следующим текстом.</span><span class="sxs-lookup"><span data-stu-id="75a0f-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="75a0f-208">Эта воронка случайным образом отправляет предложения в топологию.</span><span class="sxs-lookup"><span data-stu-id="75a0f-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="75a0f-209">Реализация сит</span><span class="sxs-lookup"><span data-stu-id="75a0f-209">Implement the bolts</span></span>

1. <span data-ttu-id="75a0f-210">Удалите существующий файл **Bolt.cs** из проекта.</span><span class="sxs-lookup"><span data-stu-id="75a0f-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="75a0f-211">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="75a0f-212">Выберите в списке **Storm Bolt** (Сито воронки) и введите имя **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="75a0f-213">Повторите этот процесс для создания второго сита с именем **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="75a0f-214">**Splitter.cs** — реализует элемент bolt, который делит предложения на отдельные слова и выдает новый поток слов.</span><span class="sxs-lookup"><span data-stu-id="75a0f-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="75a0f-215">**Counter.cs** — реализует элемент bolt, который подсчитывает каждое слово и выдает новый поток слов и частоту их употребления.</span><span class="sxs-lookup"><span data-stu-id="75a0f-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="75a0f-216">Хотя эти сита считывают данные и записывают их в потоки, их можно также использовать для взаимодействия с базой данных, службой и т. д.</span><span class="sxs-lookup"><span data-stu-id="75a0f-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="75a0f-217">Откройте файл **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="75a0f-218">Он содержит только один метод по умолчанию — **Execute**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="75a0f-219">Этот метод вызывается, когда сито получает кортеж для обработки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="75a0f-220">Здесь можно считывать и обрабатывать входящие кортежи и создавать исходящие кортежи.</span><span class="sxs-lookup"><span data-stu-id="75a0f-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="75a0f-221">Замените содержимое файла класса **Splitter** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="75a0f-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="75a0f-222">Откройте файл **Counter.cs** и замените содержимое класса следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="75a0f-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="75a0f-223">Определение топологии</span><span class="sxs-lookup"><span data-stu-id="75a0f-223">Define the topology</span></span>

<span data-ttu-id="75a0f-224">Потоки данных между компонентами могут быть представлены в виде диаграммы воронок и сит.</span><span class="sxs-lookup"><span data-stu-id="75a0f-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="75a0f-225">Граф для этой топологии выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="75a0f-225">For this topology, the graph is as follows:</span></span>

![Схема компонентов](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="75a0f-227">Предложения отправляются из компонента spout и распределяются между экземплярами элемента bolt Splitter.</span><span class="sxs-lookup"><span data-stu-id="75a0f-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="75a0f-228">Сито Splitter разбивает предложения на слова, которые распределяются среди экземпляров сита Counter.</span><span class="sxs-lookup"><span data-stu-id="75a0f-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="75a0f-229">Так как статистика хранится локально в экземпляре Counter, нужно убедиться, что определенные слова поступают в один и тот же экземпляр сита Counter.</span><span class="sxs-lookup"><span data-stu-id="75a0f-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="75a0f-230">Каждое конкретное слово отслеживается только одним экземпляром.</span><span class="sxs-lookup"><span data-stu-id="75a0f-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="75a0f-231">Так как сито Splitter не поддерживает состояние, на самом деле неважно, какое предложение получает то или иное сито.</span><span class="sxs-lookup"><span data-stu-id="75a0f-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="75a0f-232">Откройте файл **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-232">Open **Program.cs**.</span></span> <span data-ttu-id="75a0f-233">**GetTopologyBuilder** — важный метод, который используется, чтобы определить топологию, отправляющуюся в Storm.</span><span class="sxs-lookup"><span data-stu-id="75a0f-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="75a0f-234">Чтобы реализовать описанную выше топологию, замените содержимое файла **GetTopologyBuilder** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="75a0f-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="75a0f-235">Отправка топологии</span><span class="sxs-lookup"><span data-stu-id="75a0f-235">Submit the topology</span></span>

1. <span data-ttu-id="75a0f-236">В **обозревателе решений** щелкните правой кнопкой мыши проект и выберите **Submit to Storm on HDInsight** (Отправить в Storm в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="75a0f-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75a0f-237">При появлении запроса введите учетные данные для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0f-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="75a0f-238">Если у вас несколько подписок, воспользуйтесь той, что содержит ваш кластер Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="75a0f-239">Выберите Storm в кластере HDInsight из раскрывающегося списка **Кластер Storm** и щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="75a0f-240">Вы можете отслеживать выполнение отправки в окне **Выходные данные** .</span><span class="sxs-lookup"><span data-stu-id="75a0f-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="75a0f-241">После успешной отправки топологии должны появиться **топологии Storm** для кластера.</span><span class="sxs-lookup"><span data-stu-id="75a0f-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="75a0f-242">Выберите топологию **WordCount** в списке, чтобы просмотреть информацию о выполняемой топологии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75a0f-243">**Топологии Storm** можно также просмотреть в **обозревателе сервера**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="75a0f-244">Разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши элемент "Storm" в кластере HDInsight и выберите пункт **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="75a0f-245">Чтобы просмотреть сведения о компонентах в топологии, дважды щелкните компонент на схеме.</span><span class="sxs-lookup"><span data-stu-id="75a0f-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="75a0f-246">В представлении **Topology Summary** (Сводка по топологии) выберите **Kill** (Удалить), чтобы остановить топологию.</span><span class="sxs-lookup"><span data-stu-id="75a0f-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75a0f-247">Топологии Storm выполняются, пока не будут удалены или пока не будет удален кластер.</span><span class="sxs-lookup"><span data-stu-id="75a0f-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="75a0f-248">Транзакционная топология</span><span class="sxs-lookup"><span data-stu-id="75a0f-248">Transactional topology</span></span>

<span data-ttu-id="75a0f-249">Предыдущая топология является нетранзакционной.</span><span class="sxs-lookup"><span data-stu-id="75a0f-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="75a0f-250">Компоненты топологии не реализуют функциональные возможности для воспроизведения сообщений.</span><span class="sxs-lookup"><span data-stu-id="75a0f-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="75a0f-251">Чтобы получить пример транзакционной топологии, создайте проект и выберите в качестве типа проекта **Пример Storm**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="75a0f-252">Транзакционные топологии реализуют следующие возможности, обеспечивающие воспроизведение данных:</span><span class="sxs-lookup"><span data-stu-id="75a0f-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="75a0f-253">**Кэширование метаданных** — в компоненте spout должны храниться метаданные для отправляемых данных, чтобы их можно было извлечь и отправить повторно в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="75a0f-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="75a0f-254">Так как в этом примере отправляются данные небольшого размера, необработанные данные каждого кортежа хранятся в словаре для воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="75a0f-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="75a0f-255">**Подтверждение** — каждый элемент bolt в топологии может вызвать `this.ctx.Ack(tuple)`, чтобы подтвердить успешную обработку кортежа.</span><span class="sxs-lookup"><span data-stu-id="75a0f-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="75a0f-256">Как только все сита подтвердят обработку кортежа, для воронки вызывается метод `Ack` .</span><span class="sxs-lookup"><span data-stu-id="75a0f-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="75a0f-257">Метод `Ack` позволяет воронке удалить кэшированные данные для воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="75a0f-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="75a0f-258">**Fail** (Сбой) — каждое сито может вызвать `this.ctx.Fail(tuple)`, указав тем самым на сбой при обработке кортежа.</span><span class="sxs-lookup"><span data-stu-id="75a0f-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="75a0f-259">Информация о сбое передается в метод `Fail` воронки, в которой кортеж может быть воспроизведен с помощью кэшированных метаданных.</span><span class="sxs-lookup"><span data-stu-id="75a0f-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="75a0f-260">**Sequence ID**(Идентификатор последовательности) — при отправке кортежа может быть указан уникальный идентификатор последовательности.</span><span class="sxs-lookup"><span data-stu-id="75a0f-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="75a0f-261">Это значение, по которому кортеж можно идентифицировать для обработки воспроизведения (подтверждения и сбоя).</span><span class="sxs-lookup"><span data-stu-id="75a0f-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="75a0f-262">Например, воронка в проекте **Storm Sample** (Пример Storm) при отправке данных использует следующий код:</span><span class="sxs-lookup"><span data-stu-id="75a0f-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="75a0f-263">При этом в заданный по умолчанию поток отправляется кортеж, содержащий предложение. Значение идентификатора последовательности содержится в **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="75a0f-264">В этом примере **lastSeqId** увеличивается после каждой отправки кортежа.</span><span class="sxs-lookup"><span data-stu-id="75a0f-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="75a0f-265">Как показано в проекте **Пример Storm**, транзакционность компонента можно задать во время выполнения в соответствии с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="75a0f-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="75a0f-266">Гибридная топология с помощью C# и Java</span><span class="sxs-lookup"><span data-stu-id="75a0f-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="75a0f-267">Средства Data Lake для Visual Studio можно также использовать для создания гибридных топологий, в которых одни компоненты написаны на C#, а другие — на Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="75a0f-268">Чтобы получить пример гибридной топологии, создайте проект и выберите **Пример гибридного решения Storm**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="75a0f-269">В примере демонстрируются следующие понятия:</span><span class="sxs-lookup"><span data-stu-id="75a0f-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="75a0f-270">**Компонент spout на Java** и **элемент bolt на C#** — определены в **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="75a0f-271">Транзакционная версия определена в **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="75a0f-272">**Компонент spout на C#** и **элемент bolt на Java** — определены в **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="75a0f-273">Транзакционная версия определена в **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="75a0f-274">В этой версии также демонстрируется использование кода Clojure из текстового файла в качестве компонента Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="75a0f-275">Для переключения топологии, используемой при отправке проекта, перед отправкой в кластер переместите оператор `[Active(true)]` в топологию, которую необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="75a0f-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="75a0f-276">Все необходимые файлы Java предоставляются в составе этого проекта и находятся в папке **JavaDependency** .</span><span class="sxs-lookup"><span data-stu-id="75a0f-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="75a0f-277">При создании и отправке гибридной топологии учитывайте указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="75a0f-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="75a0f-278">Для создания экземпляра класса Java для элемента spout или bolt необходимо использовать **JavaComponentConstructor**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="75a0f-279">Для сериализации данных в компоненты Java и из них из объектов Java в JSON необходимо использовать **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="75a0f-280">Отправляя топологию на сервер, необходимо использовать параметр **Дополнительные конфигурации**, чтобы задать **пути к файлам Java**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="75a0f-281">При этом следует указать путь к каталогу, содержащему JAR-файлы с классами Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="75a0f-282">Концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="75a0f-282">Azure Event Hubs</span></span>

<span data-ttu-id="75a0f-283">В SCP.NET версии 0.9.4.203 появились новые класс и метод, предназначенные специально для работы с компонентом spout концентратора событий (компонентом spout Java, который считывает данные из концентраторов событий).</span><span class="sxs-lookup"><span data-stu-id="75a0f-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="75a0f-284">При создании топологии, которая использует компонент spout концентратора событий, используйте указанные ниже методы.</span><span class="sxs-lookup"><span data-stu-id="75a0f-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="75a0f-285">Класс **EventHubSpoutConfig**. Создает объект, который содержит настройки для компонента spout.</span><span class="sxs-lookup"><span data-stu-id="75a0f-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="75a0f-286">Метод **TopologyBuilder.SetEventHubSpout**. Добавляет компонент spout концентратора событий к топологии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="75a0f-287">Для сериализации данных, созданных компонентом spout, необходимо по-прежнему использовать **CustomizedInteropJSONSerializer**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="75a0f-288"><a id="configurationmanager"></a>Использование ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="75a0f-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="75a0f-289">Не используйте **ConfigurationManager**, чтобы получать значения конфигурации из компонентов bolt и spout.</span><span class="sxs-lookup"><span data-stu-id="75a0f-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="75a0f-290">Это вызовет исключение пустого указателя.</span><span class="sxs-lookup"><span data-stu-id="75a0f-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="75a0f-291">Вместо этого конфигурация проекта передается в топологию Storm как пара "ключ — значение" в контексте топологии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="75a0f-292">Каждому компоненту, зависящему от значений конфигурации, необходимо получить их из контекста во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="75a0f-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="75a0f-293">В приведенном ниже коде показано, как получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="75a0f-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="75a0f-294">Если используется метод `Get`, чтобы вернуть экземпляр компонента, он должен передавать конструктору параметры `Context` и `Dictionary<string, Object>`.</span><span class="sxs-lookup"><span data-stu-id="75a0f-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="75a0f-295">В примере ниже показан базовый метод `Get`, передающий значения должным образом.</span><span class="sxs-lookup"><span data-stu-id="75a0f-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="75a0f-296">Обновление SCP.NET</span><span class="sxs-lookup"><span data-stu-id="75a0f-296">How to update SCP.NET</span></span>

<span data-ttu-id="75a0f-297">Последние версии SCP.NET поддерживают обновление пакета через NuGet.</span><span class="sxs-lookup"><span data-stu-id="75a0f-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="75a0f-298">Если доступно новое обновление, вы получите уведомление об обновлении.</span><span class="sxs-lookup"><span data-stu-id="75a0f-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="75a0f-299">Чтобы вручную проверить обновления, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="75a0f-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="75a0f-300">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="75a0f-301">Из диспетчера пакетов выберите **Обновления**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="75a0f-302">Если обновление доступно, оно будет отображено.</span><span class="sxs-lookup"><span data-stu-id="75a0f-302">If an update is available, it is listed.</span></span> <span data-ttu-id="75a0f-303">Нажмите кнопку **Обновление** для его установки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75a0f-304">Если проект был создан с помощью предыдущей версии SCP.NET, в которой не использовалось средство NuGet, выполните следующие действия для обновления до новой версии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="75a0f-305">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="75a0f-306">С помощью поля **Поиск** найдите **пакет SDK Microsoft.SCP.Net.** и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="75a0f-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="75a0f-307">Устранение распространенных неполадок с топологиями</span><span class="sxs-lookup"><span data-stu-id="75a0f-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="75a0f-308">Исключение пустого указателя</span><span class="sxs-lookup"><span data-stu-id="75a0f-308">Null pointer exceptions</span></span>

<span data-ttu-id="75a0f-309">При использовании топологии C# с кластером HDInsight под управлением Linux компоненты bolt и spout, считывающие параметры конфигурации с помощью **ConfigurationManager** во время выполнения, могут вернуть исключение пустого указателя.</span><span class="sxs-lookup"><span data-stu-id="75a0f-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="75a0f-310">Конфигурация проекта передается в топологию Storm как пара "ключ —значение" в контексте топологии.</span><span class="sxs-lookup"><span data-stu-id="75a0f-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="75a0f-311">Ее можно извлечь из объекта dictionary, который передается в компоненты при их инициализации.</span><span class="sxs-lookup"><span data-stu-id="75a0f-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="75a0f-312">Дополнительные сведения см. в этой статье в разделе [ConfigurationManager](#configurationmanager).</span><span class="sxs-lookup"><span data-stu-id="75a0f-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="75a0f-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="75a0f-313">System.TypeLoadException</span></span>

<span data-ttu-id="75a0f-314">При использовании топологии C# с кластером HDInsight под управлением Linux может возникнуть следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="75a0f-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="75a0f-315">Она происходит, когда используется двоичный файл, несовместимый с версией .NET, поддерживающей Mono.</span><span class="sxs-lookup"><span data-stu-id="75a0f-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="75a0f-316">Для кластеров HDInsight под управлением Linux в проекте должны использоваться двоичные файлы, скомпилированные для .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="75a0f-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="75a0f-317">Локальная проверка топологии</span><span class="sxs-lookup"><span data-stu-id="75a0f-317">Test a topology locally</span></span>

<span data-ttu-id="75a0f-318">Хотя топологию легко развернуть в кластер, иногда ее необходимо проверять локально.</span><span class="sxs-lookup"><span data-stu-id="75a0f-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="75a0f-319">Чтобы запустить и протестировать пример топологии, описанной в этой статье, локально в среде разработки, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="75a0f-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="75a0f-320">Локальное тестирование работает только для базовых топологий на C#.</span><span class="sxs-lookup"><span data-stu-id="75a0f-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="75a0f-321">Нельзя использовать локальное тестирование для гибридных топологий или топологий, использующих несколько потоков.</span><span class="sxs-lookup"><span data-stu-id="75a0f-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="75a0f-322">В **обозревателе решений** щелкните правой кнопкой мыши проект и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="75a0f-323">В свойствах проекта измените **Тип выходных данных** на **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Снимок экрана: свойства проекта с выделенным свойством "Тип выходных данных"](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="75a0f-325">Перед развертыванием топологии в кластере не забудьте вернуть для параметра **Тип выходных данных** значение **Библиотеки классов**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="75a0f-326">В **обозревателе решений** щелкните правой кнопкой мыши проект, а затем выберите **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="75a0f-327">Щелкните **Класс** и введите имя класса **LocalTest.cs**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="75a0f-328">Теперь нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="75a0f-329">Откройте класс **LocalTest.cs** и добавьте в начало следующий оператор **using**:</span><span class="sxs-lookup"><span data-stu-id="75a0f-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="75a0f-330">Вставьте в класс **LocalTest** следующий код:</span><span class="sxs-lookup"><span data-stu-id="75a0f-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="75a0f-331">Ознакомьтесь с комментариями в коде.</span><span class="sxs-lookup"><span data-stu-id="75a0f-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="75a0f-332">В этом коде для запуска компонентов в среде разработки используется **LocalContext**. При этом поток данных сохраняется между компонентами текстовых файлов на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="75a0f-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="75a0f-333">Откройте **Program.cs** и добавьте в метод **Main** следующий код:</span><span class="sxs-lookup"><span data-stu-id="75a0f-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="75a0f-334">Сохраните изменения, а затем нажмите клавишу **F5** или щелкните **Отладка** > **Начать отладку**, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="75a0f-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="75a0f-335">Должно появится окно консоли, а также данные о состоянии журнала в ходе выполнения тестов.</span><span class="sxs-lookup"><span data-stu-id="75a0f-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="75a0f-336">Когда появится надпись **Тесты завершены** , нажмите любую клавишу, чтобы закрыть окно.</span><span class="sxs-lookup"><span data-stu-id="75a0f-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="75a0f-337">Используйте **проводник** для поиска каталога, который содержит проект,</span><span class="sxs-lookup"><span data-stu-id="75a0f-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="75a0f-338">например **C:\Users\<имя_пользователя>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="75a0f-339">В этом каталоге откройте **Bin**, а затем щелкните **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="75a0f-340">Отобразятся текстовые файлы, которые были созданы во время выполнения тестов: sentences.txt, counter.txt и splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="75a0f-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="75a0f-341">Откройте каждый текстовый файл и проверьте данные.</span><span class="sxs-lookup"><span data-stu-id="75a0f-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75a0f-342">Строковые данные сохраняются в этих файлах как массив значений типа decimal.</span><span class="sxs-lookup"><span data-stu-id="75a0f-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="75a0f-343">Например, \[[97,103,111]] в файле **splitter.txt** — это слово *and*.</span><span class="sxs-lookup"><span data-stu-id="75a0f-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="75a0f-344">Перед развертыванием в Storm в кластере HDInsight не забудьте вернуть для параметра **Тип проекта** значение **Библиотека классов**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="75a0f-345">Информация о журнале</span><span class="sxs-lookup"><span data-stu-id="75a0f-345">Log information</span></span>

<span data-ttu-id="75a0f-346">С помощью `Context.Logger`можно легко записывать информацию из компонентов топологии в журнал.</span><span class="sxs-lookup"><span data-stu-id="75a0f-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="75a0f-347">Например, приведенный ниже код создаст информационную запись в журнале:</span><span class="sxs-lookup"><span data-stu-id="75a0f-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="75a0f-348">Записанную информацию можно просмотреть в **журнале службы Hadoop**, который можно найти в **обозревателе сервера**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="75a0f-349">Разверните запись для Storm в кластере HDInsight, а затем — **Журнал службы Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="75a0f-350">Выберите файла журнала для просмотра.</span><span class="sxs-lookup"><span data-stu-id="75a0f-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="75a0f-351">Журналы хранятся в используемой в кластере учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="75a0f-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="75a0f-352">Для просмотра журналов в Visual Studio необходимо войти в подписку Azure, содержащую эту учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="75a0f-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="75a0f-353">Просмотр информации об ошибке</span><span class="sxs-lookup"><span data-stu-id="75a0f-353">View error information</span></span>

<span data-ttu-id="75a0f-354">Чтобы просмотреть ошибки, произошедшие в работающей топологии, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="75a0f-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="75a0f-355">В **обозревателе сервера** щелкните правой кнопкой мыши Storm в кластере HDInsight и выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="75a0f-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="75a0f-356">Для элементов **spout** и **bolt** столбец **Последняя ошибка** содержит сведения о последней ошибке.</span><span class="sxs-lookup"><span data-stu-id="75a0f-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="75a0f-357">Выберите **идентификатор воронки** или **идентификатор сита** для компонента с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="75a0f-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="75a0f-358">На отобразившейся странице подробностей в разделе **Ошибки** в нижней части страницы указаны дополнительные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="75a0f-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="75a0f-359">Дополнительные сведения можно получить, выбрав **Порт** в разделе **Исполнители** на этой странице и просмотрев журнал рабочих процессов Storm за последние несколько минут.</span><span class="sxs-lookup"><span data-stu-id="75a0f-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="75a0f-360">Ошибки при отправке топологии</span><span class="sxs-lookup"><span data-stu-id="75a0f-360">Errors submitting topologies</span></span>

<span data-ttu-id="75a0f-361">Если при отправке топологии в HDInsight возникают ошибки, можно найти журналы для серверных компонентов, которые обрабатывают отправку топологии в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="75a0f-362">Чтобы получить эти журналы, выполните следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="75a0f-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="75a0f-363">Замените __sshuser__ именем учетной записи пользователя SSH для кластера.</span><span class="sxs-lookup"><span data-stu-id="75a0f-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="75a0f-364">Замените __clustername__ именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="75a0f-365">Дополнительные сведения об использовании `scp` и `ssh` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="75a0f-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="75a0f-366">Отправка может завершиться ошибкой по нескольким причинам:</span><span class="sxs-lookup"><span data-stu-id="75a0f-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="75a0f-367">Пакет JDK не установлен или не находится по требуемому пути.</span><span class="sxs-lookup"><span data-stu-id="75a0f-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="75a0f-368">Необходимые зависимости Java не включены в отправляемые данные.</span><span class="sxs-lookup"><span data-stu-id="75a0f-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="75a0f-369">Несовместимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="75a0f-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="75a0f-370">Повторяющиеся имена топологий.</span><span class="sxs-lookup"><span data-stu-id="75a0f-370">Duplicate topology names.</span></span>

<span data-ttu-id="75a0f-371">Если журнал `hdinsight-scpwebapi.out` содержит `FileNotFoundException`, это может быть вызвано указанными ниже причинами.</span><span class="sxs-lookup"><span data-stu-id="75a0f-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="75a0f-372">Пакет JDK не находится по требуемому пути в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="75a0f-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="75a0f-373">Убедитесь в том, что пакет JDK установлен в среде разработки, а `%JAVA_HOME%/bin` находится по требуемому пути.</span><span class="sxs-lookup"><span data-stu-id="75a0f-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="75a0f-374">Отсутствует зависимость Java.</span><span class="sxs-lookup"><span data-stu-id="75a0f-374">You are missing a Java dependency.</span></span> <span data-ttu-id="75a0f-375">Убедитесь в том, что все необходимые файлы JAR включены в отправляемые данные.</span><span class="sxs-lookup"><span data-stu-id="75a0f-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75a0f-376">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75a0f-376">Next steps</span></span>

<span data-ttu-id="75a0f-377">Пример обработки данных из концентраторов событий см. в статье [Обработка событий из концентраторов событий Azure с помощью Storm в HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="75a0f-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="75a0f-378">Пример топологии C#, которая разбивает поток данных на несколько потоков, см. на странице с [примером C# Storm](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="75a0f-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="75a0f-379">Дополнительные сведения о создании топологий C# см. в [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="75a0f-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="75a0f-380">Другие методы работы с HDInsight и дополнительные примеры Storm в HDInsight см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="75a0f-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="75a0f-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="75a0f-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="75a0f-382">Руководство по программированию для SCP</span><span class="sxs-lookup"><span data-stu-id="75a0f-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="75a0f-383">**Apache Storm в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="75a0f-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="75a0f-384">Развертывание и мониторинг топологии с помощью Apache Storm в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="75a0f-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="75a0f-385">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="75a0f-386">**Apache Hadoop в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="75a0f-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="75a0f-387">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="75a0f-388">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="75a0f-389">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="75a0f-390">**Apache HBase в HDInsight**</span><span class="sxs-lookup"><span data-stu-id="75a0f-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="75a0f-391">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75a0f-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
