---
title: "aaaSerialize данные в Hadoop - библиотеки Microsoft Avro - Azure | Документы Microsoft"
description: "Узнайте, как tooserialize и десериализовать данные в Hadoop в HDInsight с помощью toomemory toopersist hello библиотеку Microsoft Avro Library, базы данных или файла."
keywords: avro,hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="2cfc4-104">Сериализация данных в Hadoop с hello библиотеки Microsoft Avro</span><span class="sxs-lookup"><span data-stu-id="2cfc4-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="2cfc4-105">Hello Avro SDK больше не поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="2cfc4-106">Библиотека Hello является открытой поддерживается сообществом разработчиков.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-106">hello library is open source community supported.</span></span> <span data-ttu-id="2cfc4-107">Hello источников для библиотеки hello расположены в [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="2cfc4-108">В этом разделе показано, как toouse hello [библиотеки Microsoft Avro](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize объектов и других данных структуры в потоки toopersist их toomemory, базы данных или файла.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="2cfc4-109">Здесь также показано, как toodeserialize их toorecover hello исходных объектов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="2cfc4-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="2cfc4-110">Apache Avro</span></span>
<span data-ttu-id="2cfc4-111">Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">библиотеки Microsoft Avro</a> Здравствуйте, реализует систему сериализации данных Apache Avro для hello Microsoft.NET среды.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="2cfc4-112">Apache Avro обеспечивает компактный формат обмена двоичными данными для сериализации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="2cfc4-113">Она использует <a href="http://www.json.org" target="_blank">JSON</a> toodefine от языка схемы, underwrites взаимодействие между языками.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="2cfc4-114">Данные, сериализованные в одном языке, могут быть прочитаны в другом.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="2cfc4-115">В настоящее время поддерживаются C, C++, C#, Java, PHP, Python и Ruby.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="2cfc4-116">Подробные сведения о формате hello можно найти в hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro спецификации</a>.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="2cfc4-117">Hello библиотеки Microsoft Avro поддерживает hello удаленной процедуры вызовы (RPC) часть данной спецификации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="2cfc4-118">представление Hello сериализации объекта в системе Avro hello состоит из двух частей: схемы и фактическое значение.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="2cfc4-119">схемы Avro Hello описывается модель данных зависит от языка программирования hello hello сериализации данных с JSON.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="2cfc4-120">Она представлена параллельно с двоичным представлением данных.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="2cfc4-121">Наличие отдельно от hello двоичное представление схемы hello разрешает toobe каждого объекта, записанных с затратами не-значение, делая сериализации быстрое и hello представление небольшой.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="2cfc4-122">сценарий Hadoop Hello</span><span class="sxs-lookup"><span data-stu-id="2cfc4-122">hello Hadoop scenario</span></span>
<span data-ttu-id="2cfc4-123">формат сериализации Apache Avro Hello широко используется в других средах Apache Hadoop и Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="2cfc4-124">Avro предоставляет toorepresent удобный способ сложные структуры данных в задание Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="2cfc4-125">Hello формат файлов Avro (файл контейнера объекта Avro) был спроектированный toosupport hello распределенных MapReduce программной модели.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="2cfc4-126">ключевой особенностью Hello, включающий распределение hello является «разбить таблицу» в смысле hello, один поиска любой точки в файле и приступить к чтению из определенного блока hello файлы.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="2cfc4-127">Сериализация в библиотеке Avro</span><span class="sxs-lookup"><span data-stu-id="2cfc4-127">Serialization in Avro Library</span></span>
<span data-ttu-id="2cfc4-128">Hello библиотеки .NET для Avro поддерживает два способа сериализации объектов:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="2cfc4-129">**отражение** -hello схему JSON для типов hello автоматически строится на основе данных hello атрибуты контракта hello .NET типы toobe сериализации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="2cfc4-130">**Универсальный записи** -схема JSON явно указан в записи, представленный hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) класса при типы .NET не существует схема hello toodescribe для toobe данных hello сериализовать.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="2cfc4-131">Если схема данных hello известен tooboth hello записи и чтения потока hello, hello данных могут отправляться без его схемы.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="2cfc4-132">В случаях, когда используется файл Avro объекта контейнера, hello схема сохраняется в файле hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="2cfc4-133">Можно указать другие параметры, такие как hello кодек, использующийся для сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="2cfc4-134">Эти сценарии являются более подробно описано и показано в следующих примерах кода hello:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="2cfc4-135">Установка библиотеки Avro</span><span class="sxs-lookup"><span data-stu-id="2cfc4-135">Install Avro Library</span></span>
<span data-ttu-id="2cfc4-136">требуются следующие Hello сертификаты, прежде чем устанавливать hello библиотеки:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="2cfc4-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="2cfc4-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="2cfc4-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="2cfc4-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="2cfc4-139">Обратите внимание, что hello зависимостей Newtonsoft.Json.dll автоматически загружается с установкой hello hello библиотеки Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="2cfc4-140">процедура Hello представлен в следующем разделе hello:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="2cfc4-141">Hello библиотеку Microsoft Avro Library распространяется в виде пакета NuGet, который можно установить из Visual Studio через hello следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="2cfc4-142">Выберите hello **проекта** -> вкладка **управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="2cfc4-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="2cfc4-143">Поиск «Microsoft.Hadoop.Avro» в hello **поиск в Интернете** поле.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="2cfc4-144">Нажмите кнопку hello **установить** рядом слишком**библиотеку Avro Microsoft Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="2cfc4-145">Обратите внимание, что hello Newtonsoft.Json.dll (> = 6.0.4) также зависимостей автоматически загружается с hello библиотеки Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="2cfc4-146">Hello библиотеку Microsoft Avro Library исходный код доступен на [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="2cfc4-147">Компиляция схем с использованием библиотеки Avro</span><span class="sxs-lookup"><span data-stu-id="2cfc4-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="2cfc4-148">Hello библиотеку Microsoft Avro Library содержит создания кода, служебная программа, которая позволяет создавать типы C# автоматически на основании hello ранее определенные схемы JSON.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="2cfc4-149">Программа формирования кода Hello не поставляется как двоичный исполняемый файл, но можно легко создавать через hello после процедуры:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="2cfc4-150">Загрузки hello ZIP-файла с последней версией hello HDInsight SDK исходного кода из <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK для Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="2cfc4-151">(Щелкните hello **загрузки** значок, не hello **загружает** вкладке.)</span><span class="sxs-lookup"><span data-stu-id="2cfc4-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="2cfc4-152">Извлеките hello каталог tooa HDInsight SDK на компьютере hello с .NET Framework 4 установлена и подключена toohello Интернет для загрузки пакетов NuGet необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="2cfc4-153">Ниже мы предполагаем, что hello исходный код находится извлеченный tooC:\SDK.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="2cfc4-154">Перейдите в папку toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools и запустите build.bat.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="2cfc4-155">(hello файл вызовы MSBuild из 32-разрядных распределение hello hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="2cfc4-156">Если требуется 64-разрядная версия toouse hello редактировать build.bat, следуя hello комментарии в файле hello.) Убедитесь, что hello построение выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="2cfc4-157">(В некоторых системах MSBuild может создавать предупреждения.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="2cfc4-158">Эти предупреждения не влияют на приветствия программы при условии, что отсутствуют ошибки построения.)</span><span class="sxs-lookup"><span data-stu-id="2cfc4-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="2cfc4-159">Служебная программа Hello компиляции находится в C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="2cfc4-160">tooget знакомы с hello синтаксис командной строки, выполните следующую команду из папки hello, где находится служебная программа для создания кода hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="2cfc4-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="2cfc4-161">Программа hello tootest, можно создать классов C# из hello образца JSON схемы файла с исходным кодом hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="2cfc4-162">Выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="2cfc4-163">Это должно tooproduce два файла C# в текущем каталоге hello: SensorData.cs и Location.cs.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="2cfc4-164">toounderstand hello логику, которая использует программа создания кода hello при преобразовании типов tooC # hello JSON схемы, см. файл hello GenerationVerification.feature, расположенный в C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="2cfc4-165">Пространства имен, извлекаются из схемы JSON hello, с помощью логики hello, описанных в файле hello, упомянутые в предыдущем абзаце hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="2cfc4-166">Пространства имен, извлеченных из схемы hello имеют приоритет над все, что входит в состав параметр /n hello в hello служебной программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="2cfc4-167">Если вы хотите hello toooverride пространства имен, содержащиеся в схеме hello, используйте параметр /nf hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="2cfc4-168">Например, toochange все пространства имен из hello SampleJSONSchema.avsc toomy.own.nspace, выполнить hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="2cfc4-169">Об образцах hello</span><span class="sxs-lookup"><span data-stu-id="2cfc4-169">About hello samples</span></span>
<span data-ttu-id="2cfc4-170">Шесть примеры, приведенные в этом разделе иллюстрируют различные сценарии, поддерживаемые hello библиотеки Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="2cfc4-171">Hello библиотеку Microsoft Avro Library — спроектированный toowork с любой поток.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="2cfc4-172">В этих примерах для простоты и последовательности управление данными осуществляется с использованием потоков в памяти, а не файловых потоков или баз данных.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="2cfc4-173">Hello подходов, использованных в рабочей среде зависит от требований конкретного сценария hello, источник данных и тома, ограничения производительности и других факторов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="2cfc4-174">Здравствуйте первый двух примерах показано, как tooserialize и десериализации данных в памяти буферы потока с помощью отражение и универсальные записей.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="2cfc4-175">Hello схемы в этих двух случаях предполагается toobe совместно hello средств чтения и записи по каналу.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="2cfc4-176">Hello третья и четвертая примеры как tooserialize и десериализации данных с помощью объекта контейнера hello Avro файлов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="2cfc4-177">Если данные хранятся в файле Avro контейнер, его схемы всегда хранится вместе с ним, поскольку hello схемы должны быть общими для десериализации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="2cfc4-178">Hello содержащий образец hello первые четыре примеры можно загрузить из hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">образцы кода Azure</a> сайта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="2cfc4-179">Hello пятый примере показан способ toouse кодек сжатия для Avro объекта контейнера файлов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="2cfc4-180">Образец, содержащий код hello для в этом примере можно загрузить из hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">образцы кода Azure</a> сайта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="2cfc4-181">Hello шестой образце показано, как toouse Avro сериализации tooupload данных tooAzure хранилище больших двоичных объектов, а затем проанализировать его с помощью Hive кластера HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="2cfc4-182">Ее можно загрузить из hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">образцы кода Azure</a> сайта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="2cfc4-183">Ниже приведены ссылки toohello шесть образцы, описанные в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="2cfc4-184"><a href="#Scenario1">**Сериализация с отражением** </a> -hello схему JSON для сериализации toobe типов автоматически строится на основе данных hello атрибутов контракта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="2cfc4-185"><a href="#Scenario2">**Сериализации с помощью универсального записи** </a> -hello схемы JSON при задан явно в записи тип .NET, не доступны для отражения.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="2cfc4-186"><a href="#Scenario3">**Сериализации с помощью объекта контейнера файлов с отражением** </a> -схемы JSON hello автоматически создаваемый и общих вместе с данными сериализации hello через файл Avro объекта контейнера.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="2cfc4-187"><a href="#Scenario4">**Сериализации с помощью объекта контейнера файлов с записью универсального** </a> -схемы JSON hello явно задан перед выполнением сериализации hello и общих вместе с данными hello через файл Avro объекта контейнера.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="2cfc4-188"><a href="#Scenario5">**Сериализации с помощью объекта контейнера файлов с использованием кодека сжатия** </a> -hello примере показано, как toocreate Avro объектного файла контейнера с пользовательской реализации кодек сжатия данных Deflate hello .NET.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="2cfc4-189"><a href="#Scenario6">**Использование данных Avro tooupload hello службы Microsoft Azure HDInsight** </a> -пример hello иллюстрирует способ сериализации Avro взаимодействия с hello службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="2cfc4-190">Активные Azure подписки и доступа tooan кластера Azure HDInsight требуется toorun в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="2cfc4-191"><a name="Scenario1"></a>Пример 1. Сериализация с помощью отражения</span><span class="sxs-lookup"><span data-stu-id="2cfc4-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="2cfc4-192">Hello схему JSON для типов hello автоматически создается с hello библиотеку Microsoft Avro Library через отражение из данных hello атрибуты контракта hello C# объекты toobe сериализации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="2cfc4-193">Hello библиотеку Microsoft Avro Library создает [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello поля toobe сериализации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="2cfc4-194">В этом примере объекты ( **SensorData** класса с членом **расположение** struct) являются tooa сериализованный поток памяти и в свою очередь десериализации данного потока.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="2cfc4-195">Hello результат равен то сравниваемых toohello исходный экземпляр tooconfirm, hello **SensorData** восстановить объект имеет одинаковые toohello исходного.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="2cfc4-196">Схема Hello в этом примере предполагается, что toobe совместно hello средствами чтения и записи, поэтому формат контейнера объекта Avro hello не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="2cfc4-197">Пример того, как tooserialize и десериализации данных в буферы памяти с помощью отражения с форматом контейнера hello объекта при hello схемы должны быть общими данными hello, в разделе <a href="#Scenario3">сериализации с помощью объекта контейнера файлов с отражением</a>.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="2cfc4-198">Пример 2. Сериализация с помощью универсальной записи</span><span class="sxs-lookup"><span data-stu-id="2cfc4-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="2cfc4-199">Схема JSON можно явно указать универсальный записи при отражения не может использоваться, поскольку hello данных не могут быть представлены через классы .NET с контрактом данных.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="2cfc4-200">Этот метод занимает больше времени, чем использование отражения.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-200">This method is slower than using reflection.</span></span> <span data-ttu-id="2cfc4-201">В таких случаях hello схему для данных hello также могут быть динамическим, то есть не известна во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="2cfc4-202">Данные представлены в виде значения с разделителями запятыми (CSV) файлы, схема остается неизвестным до его преобразования формата Avro toohello во время выполнения является примером такого рода динамический сценарий.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="2cfc4-203">В этом примере показано, как toocreate и использовать [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly указания схемы JSON, как toopopulate его с данными hello, а затем как tooserialize и десериализацию.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="2cfc4-204">Hello результат затем сравнивается tooconfirm toohello исходный экземпляр, hello восстановить запись имеет идентичные toohello исходного.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="2cfc4-205">Схема Hello в этом примере предполагается, что toobe совместно hello средствами чтения и записи, поэтому формат контейнера объекта Avro hello не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="2cfc4-206">Пример того, как tooserialize и десериализации данных в буферы памяти с помощью универсального записи с форматом контейнера hello объекта при hello схемы должен быть включен с hello сериализации данных, в разделе hello <a href="#Scenario4">сериализации с помощью объекта контейнера файлы с записью универсального</a> примере.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="2cfc4-207">Пример 3. Сериализация с помощью файлов контейнеров объектов и сериализация с помощью отражения</span><span class="sxs-lookup"><span data-stu-id="2cfc4-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="2cfc4-208">Данный пример является похожее toohello в hello <a href="#Scenario1"> в первом примере</a>, где hello схемы неявно определяется с помощью отражения.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="2cfc4-209">Hello различие состоит в том, hello схемы не предполагается toobe известные toohello чтения, которое десериализует его.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="2cfc4-210">Hello **SensorData** сериализации toobe объекты и их неявно указанной схемы хранятся в файл контейнера Avro объекта, представленного hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) класс.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="2cfc4-211">Hello данных сериализуется в этом примере с [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) и десериализации с [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="2cfc4-212">результат Hello то сравниваемых toohello начальных экземпляров tooensure удостоверений.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="2cfc4-213">Hello данные в hello объекта сжатии контейнера по умолчанию hello [ **Deflate** ] [ deflate-100] кодек сжатия с .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="2cfc4-214">В разделе hello <a href="#Scenario5"> пятого примера</a> в этой статье toolearn как toouse более новую и более высокой версии hello [ **Deflate** ] [ deflate-110] сжатия кодек, доступных в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="2cfc4-215">Пример 4. Сериализация с помощью файлов контейнеров объектов и сериализация с помощью универсальной записи</span><span class="sxs-lookup"><span data-stu-id="2cfc4-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="2cfc4-216">Данный пример является похожее toohello в hello <a href="#Scenario2"> во втором примере</a>, где явно указана схема hello с JSON.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="2cfc4-217">Hello различие состоит в том, hello схемы не предполагается toobe известные toohello чтения, которое десериализует его.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="2cfc4-218">Hello проверочных данных собираются в список [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) объектов через явно определенной схемой JSON, а затем сохраняются в файл контейнера объекта, представленного hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="2cfc4-219">Этот файл контейнер создает записи, — это данные, используемые tooserialize hello, несжатых данных, поток памяти tooa, затем сохраняется файл tooa.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="2cfc4-220">Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) параметр, используемый для создания средства чтения hello указывает, что эти данные не сжимается.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="2cfc4-221">Hello данных считывается из файла hello и десериализации в коллекции объектов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="2cfc4-222">Эта коллекция является первоначальный список сравниваемых toohello tooconfirm записи Avro, что они совпадают.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="2cfc4-223">Пример 5. Сериализация с использованием файлов контейнеров объектов с помощью настраиваемого кодека сжатия</span><span class="sxs-lookup"><span data-stu-id="2cfc4-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="2cfc4-224">Hello пятый примере показан способ toouse кодек сжатия для Avro объекта контейнера файлов.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="2cfc4-225">Образец, содержащий код hello для в этом примере можно загрузить из hello [образцы кода Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) сайта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="2cfc4-226">Hello [спецификации Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) разрешает использование кодек сжатия необязательно (кроме слишком**Null** и **Deflate** значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="2cfc4-227">В этом примере не реализует новый кодек, например Snappy (упоминается как поддерживаемые необязательные кодек в hello [Avro спецификации](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="2cfc4-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="2cfc4-228">Здесь показано, как toouse hello реализация .NET Framework 4.5 hello [ **Deflate** ] [ deflate-110] кодека, который обеспечивает более эффективный алгоритм сжатия основании hello [zlib](http://zlib.net/) библиотеки сжатия, чем версия .NET Framework 4 hello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="2cfc4-229">Пример 6: Использование данных Avro tooupload для hello службы Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2cfc4-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="2cfc4-230">Hello шестой пример иллюстрирует некоторые программирования toointeracting связанные методы со службой Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="2cfc4-231">Образец, содержащий код hello для в этом примере можно загрузить из hello [образцы кода Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) сайта.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="2cfc4-232">Образец Hello hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="2cfc4-233">Подключается tooan существующий кластер службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="2cfc4-234">Сериализует несколько CSV-файлы и отправляет хранилища больших двоичных объектов tooAzure результат hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="2cfc4-235">(hello CSV-файлы, распространяемые вместе с образец hello и представляют извлечения из AMEX Stock исторических данных, распределенных по [Infochimps](http://www.infochimps.com/) период hello 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="2cfc4-236">Образец Hello считывает данные CSV-файла, преобразует hello tooinstances записей из hello **Stock** класса, а затем выполняет сериализацию с помощью отражения.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="2cfc4-237">Определение типа биржевой создается на основе схемы JSON через hello программа создания кода библиотеки Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="2cfc4-238">Создает новую таблицу внешнего **акции** в кусте и связывает его toohello данные отправлены в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="2cfc4-239">Выполняет запрос с использованием Hive через hello **акции** таблицы.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="2cfc4-240">Кроме того образец hello выполняет процедуру очистки, до и после выполнения основных операций.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="2cfc4-241">Во время hello очистки все hello, связанные с удаляются данные больших двоичных объектов Azure и папки hello Hive таблица удаляется.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="2cfc4-242">Можно также вызвать процедуру очистки hello из командной строки образца hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="2cfc4-243">Образец Hello имеет hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="2cfc4-244">Активная подписка Microsoft Azure и ее идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="2cfc4-245">Сертификат управления для подписки hello с hello соответствующего закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="2cfc4-246">Hello сертификат должен быть установлен в hello текущего пользователя закрытого хранения на образце hello toorun компьютер, используемый hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="2cfc4-247">Активный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="2cfc4-248">Учетная запись хранилища Azure связан toohello кластер HDInsight из предыдущего необходимым условием hello, вместе с hello соответствующего доступа первичного или вторичного ключа.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="2cfc4-249">Перед запуском образца hello все сведения hello hello необходимых компонентов следует введенное toohello образец файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="2cfc4-250">Существует два способа toodo его:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="2cfc4-251">Измените файл app.config hello в корневом каталоге образца hello и затем Постройте образец hello</span><span class="sxs-lookup"><span data-stu-id="2cfc4-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="2cfc4-252">Сначала постройте образец hello, а затем измените AvroHDISample.exe.config в каталог сборки hello</span><span class="sxs-lookup"><span data-stu-id="2cfc4-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="2cfc4-253">В обоих случаях необходимо сделать все изменения в hello  **<appSettings>**  разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="2cfc4-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="2cfc4-254">Выполните hello комментарии в файле hello.</span><span class="sxs-lookup"><span data-stu-id="2cfc4-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="2cfc4-255">Hello пример запущен из командной строки hello, выполнив следующую команду (где hello ZIP-файл с примером hello признан tooC:\AvroHDISample toobe извлечь; Если в противном случае используйте hello соответствующий путь к файлу) hello:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="2cfc4-256">tooclean hello кластера, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2cfc4-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
