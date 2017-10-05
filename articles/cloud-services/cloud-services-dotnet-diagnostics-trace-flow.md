---
title: "Трассировка потока в приложении облачных служб с использованием системы диагностики Azure | Документация Майкрософт"
description: "Добавление сообщений трассировки в приложения Azure для отладки, измерения производительности, мониторинга, анализа трафика и выполнения других задач."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="337b2-103">Трассировка потока в приложении облачных служб с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="337b2-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="337b2-104">Трассировка — это мониторинг выполнения запущенного приложения.</span><span class="sxs-lookup"><span data-stu-id="337b2-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="337b2-105">Сведения об ошибках и выполнении приложений можно записывать в журналы, текстовые файлы или на устройства для последующего анализа с помощью классов [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) и [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx).</span><span class="sxs-lookup"><span data-stu-id="337b2-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="337b2-106">Дополнительные сведения о трассировке см. в статье [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx) (Трассировка и инструментирование приложений).</span><span class="sxs-lookup"><span data-stu-id="337b2-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="337b2-107">Использование трассировочных операторов и переключателей</span><span class="sxs-lookup"><span data-stu-id="337b2-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="337b2-108">Чтобы реализовать трассировку в приложении облачных служб, добавьте класс [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) в конфигурацию приложения и вызовите метод System.Diagnostics.Trace или System.Diagnostics.Debug в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="337b2-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="337b2-109">Используйте файл конфигурации *app.config* для рабочих ролей и *web.config* для веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="337b2-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="337b2-110">Во время создания размещенной службы с помощью шаблона Visual Studio система диагностики Azure автоматически добавляется в проект. При этом класс DiagnosticMonitorTraceListener включается в соответствующий файл конфигурации для добавляемых ролей.</span><span class="sxs-lookup"><span data-stu-id="337b2-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="337b2-111">Дополнительные сведения о размещении трассировочных операторов см. в статье [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx) (Добавление трассировочных операторов в код приложения).</span><span class="sxs-lookup"><span data-stu-id="337b2-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="337b2-112">Процессом и масштабом трассировки можно управлять. Для этого добавьте в код [переключатели трассировки](https://msdn.microsoft.com/library/3at424ac.aspx).</span><span class="sxs-lookup"><span data-stu-id="337b2-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="337b2-113">Так вы сможете отслеживать состояние приложения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="337b2-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="337b2-114">Это особенно важно в бизнес-приложениях, которые используют различные компоненты, выполняющиеся на нескольких компьютерах.</span><span class="sxs-lookup"><span data-stu-id="337b2-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="337b2-115">Дополнительные сведения см. в статье [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx) (Настройка переключателей трассировки).</span><span class="sxs-lookup"><span data-stu-id="337b2-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="337b2-116">Настройка прослушивателя трассировки в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="337b2-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="337b2-117">Использование элементов Trace, Debug и TraceSource предполагает настройку прослушивателей для сбора и записи отправляемых сообщений.</span><span class="sxs-lookup"><span data-stu-id="337b2-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="337b2-118">Прослушиватели собирают, хранят и перенаправляют сообщения трассировки.</span><span class="sxs-lookup"><span data-stu-id="337b2-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="337b2-119">Они направляют выходные данные трассировки в соответствующий целевой объект, например журнал, окно или текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="337b2-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="337b2-120">Система диагностики Azure использует класс [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) .</span><span class="sxs-lookup"><span data-stu-id="337b2-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="337b2-121">Перед выполнением следующей процедуры необходимо инициализировать монитор диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="337b2-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="337b2-122">Сведения о том, как это сделать, см. в статье [Включение системы диагностики Azure в облачных службах Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="337b2-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="337b2-123">Обратите внимание, что при использовании шаблонов Visual Studio конфигурация прослушивателя добавляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="337b2-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="337b2-124">Добавление прослушивателя трассировки</span><span class="sxs-lookup"><span data-stu-id="337b2-124">Add a trace listener</span></span>
1. <span data-ttu-id="337b2-125">Откройте файл web.config или app.config для своей роли.</span><span class="sxs-lookup"><span data-stu-id="337b2-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="337b2-126">Добавьте в файл следующий код.</span><span class="sxs-lookup"><span data-stu-id="337b2-126">Add the following code to the file.</span></span> <span data-ttu-id="337b2-127">Измените атрибут Version, чтобы использовать номер версии сборки, которая указана в ссылках.</span><span class="sxs-lookup"><span data-stu-id="337b2-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="337b2-128">Версия сборки не обязательно меняется с каждым выпуском пакета SDK для Azure, а только если она обновляется.</span><span class="sxs-lookup"><span data-stu-id="337b2-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="337b2-129">Убедитесь, что у вас есть ссылка проекта на сборку Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="337b2-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="337b2-130">Обновите номер версии в приведенном выше коде XML в соответствии с версией сборки Microsoft.WindowsAzure.Diagnostics, используемой в ссылке.</span><span class="sxs-lookup"><span data-stu-id="337b2-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="337b2-131">Сохраните файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="337b2-131">Save the config file.</span></span>

<span data-ttu-id="337b2-132">Дополнительные сведения о прослушивателях см. [здесь](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="337b2-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="337b2-133">Добавив прослушиватель, вы можете добавить в код трассировочные операторы.</span><span class="sxs-lookup"><span data-stu-id="337b2-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="337b2-134">Добавление трассировочного оператора в код</span><span class="sxs-lookup"><span data-stu-id="337b2-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="337b2-135">Откройте исходный файл приложения.</span><span class="sxs-lookup"><span data-stu-id="337b2-135">Open a source file for your application.</span></span> <span data-ttu-id="337b2-136">Например, файл <RoleName>.cs для рабочей роли или веб-роли.</span><span class="sxs-lookup"><span data-stu-id="337b2-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="337b2-137">Добавьте следующий оператор using, если он еще не добавлен:</span><span class="sxs-lookup"><span data-stu-id="337b2-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="337b2-138">Добавьте трассировочные операторы, чтобы записывать сведения о состоянии приложения.</span><span class="sxs-lookup"><span data-stu-id="337b2-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="337b2-139">Вывод оператора трассировки можно форматировать разными способами.</span><span class="sxs-lookup"><span data-stu-id="337b2-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="337b2-140">Дополнительные сведения об этом см. в статье [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx) (Добавление трассировочных операторов в код приложения).</span><span class="sxs-lookup"><span data-stu-id="337b2-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="337b2-141">Сохраните исходный файл.</span><span class="sxs-lookup"><span data-stu-id="337b2-141">Save the source file.</span></span>

