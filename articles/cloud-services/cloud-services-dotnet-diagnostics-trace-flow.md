---
title: "поток aaaTrace hello в приложение облачной службы с диагностикой Azure | Документы Microsoft"
description: "Добавьте трассировки сообщений tooan приложения Azure toohelp отладки, измерения производительности, мониторинга, анализа трафика и многое другое."
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
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="eb533-103">Трассировка потока hello облачные службы приложения с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="eb533-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="eb533-104">Трассировка — это способ для вас toomonitor hello выполнения приложения, пока она запущена.</span><span class="sxs-lookup"><span data-stu-id="eb533-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="eb533-105">Можно использовать hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), и [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) классы toorecord сведения об ошибках и выполнение приложения в журналы, текстовые файлы или другие устройства для последующего анализа.</span><span class="sxs-lookup"><span data-stu-id="eb533-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="eb533-106">Дополнительные сведения о трассировке см. в статье [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx) (Трассировка и инструментирование приложений).</span><span class="sxs-lookup"><span data-stu-id="eb533-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="eb533-107">Использование трассировочных операторов и переключателей</span><span class="sxs-lookup"><span data-stu-id="eb533-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="eb533-108">Реализуйте трассировку в приложении облачные службы, добавив hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello конфигурации приложения и внесения вызывает tooSystem.Diagnostics.Trace или System.Diagnostics.Debug в вашей код приложения.</span><span class="sxs-lookup"><span data-stu-id="eb533-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="eb533-109">Использование файла конфигурации hello *app.config* для рабочих ролей и hello *web.config* для веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="eb533-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="eb533-110">При создании новой размещенной службы с помощью шаблона Visual Studio автоматически добавляется проект toohello диагностики Azure и hello DiagnosticMonitorTraceListener добавляется toohello соответствующий файл конфигурации для hello ролей, которые вы добавляете.</span><span class="sxs-lookup"><span data-stu-id="eb533-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="eb533-111">Сведения о размещении операторов трассировки см. в разделе [как: добавление операторов трассировки tooApplication кода](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb533-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="eb533-112">Процессом и масштабом трассировки можно управлять. Для этого добавьте в код [переключатели трассировки](https://msdn.microsoft.com/library/3at424ac.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb533-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="eb533-113">Это позволяет отслеживать состояние приложения в производственной среде hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="eb533-114">Это особенно важно в бизнес-приложениях, которые используют различные компоненты, выполняющиеся на нескольких компьютерах.</span><span class="sxs-lookup"><span data-stu-id="eb533-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="eb533-115">Дополнительные сведения см. в статье [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx) (Настройка переключателей трассировки).</span><span class="sxs-lookup"><span data-stu-id="eb533-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="eb533-116">Настройте прослушиватель трассировки hello в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="eb533-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="eb533-117">Trace, Debug и TraceSource, требуют настройки toocollect «прослушиватели» и сообщения hello записей, которые были отправлены.</span><span class="sxs-lookup"><span data-stu-id="eb533-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="eb533-118">Прослушиватели собирают, хранят и перенаправляют сообщения трассировки.</span><span class="sxs-lookup"><span data-stu-id="eb533-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="eb533-119">Они направлять hello трассировки вывода tooan соответствующему целевому объекту, например журнал, окно или текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="eb533-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="eb533-120">Диагностика Azure использует hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="eb533-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="eb533-121">Перед выполнением процедуры hello необходимо инициализировать монитор диагностики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="eb533-122">toodo это, см. в разделе [включение диагностики в Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="eb533-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="eb533-123">Обратите внимание, что при использовании hello шаблонов, предоставляемых средой Visual Studio, конфигурации hello hello прослушивателя добавляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="eb533-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="eb533-124">Добавление прослушивателя трассировки</span><span class="sxs-lookup"><span data-stu-id="eb533-124">Add a trace listener</span></span>
1. <span data-ttu-id="eb533-125">Откройте файл web.config или app.config hello для вашей роли.</span><span class="sxs-lookup"><span data-stu-id="eb533-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="eb533-126">Добавьте следующие toohello файл кода hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-126">Add hello following code toohello file.</span></span> <span data-ttu-id="eb533-127">Измените hello атрибут toouse hello версии номер версии hello сборки, на которую имеются ссылки.</span><span class="sxs-lookup"><span data-stu-id="eb533-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="eb533-128">версия сборки Hello не обязательно изменяет с каждым выпуском пакета Azure SDK только при наличии обновлений tooit.</span><span class="sxs-lookup"><span data-stu-id="eb533-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
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
   > <span data-ttu-id="eb533-129">Убедитесь, что у вас есть toohello ссылки проекта Microsoft.WindowsAzure.Diagnostics сборки.</span><span class="sxs-lookup"><span data-stu-id="eb533-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="eb533-130">Номер версии обновления hello в xml hello выше версии hello toomatch hello связанной сборки Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="eb533-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="eb533-131">Сохраните файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-131">Save hello config file.</span></span>

<span data-ttu-id="eb533-132">Дополнительные сведения о прослушивателях см. [здесь](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb533-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="eb533-133">После завершения tooadd hello hello действия прослушивателя, можно добавить код tooyour операторы трассировки.</span><span class="sxs-lookup"><span data-stu-id="eb533-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="eb533-134">Инструкция tooyour tooadd трассировки кода</span><span class="sxs-lookup"><span data-stu-id="eb533-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="eb533-135">Откройте исходный файл приложения.</span><span class="sxs-lookup"><span data-stu-id="eb533-135">Open a source file for your application.</span></span> <span data-ttu-id="eb533-136">Например, hello <RoleName>CS-файл для hello рабочей роли или веб-роли.</span><span class="sxs-lookup"><span data-stu-id="eb533-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="eb533-137">Добавьте следующее hello с помощью инструкции, если он уже не был добавлен:</span><span class="sxs-lookup"><span data-stu-id="eb533-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="eb533-138">Добавьте инструкции Trace место toocapture сведения о состоянии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="eb533-139">Можно использовать различные методы tooformat hello выходные данные операторов трассировки hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="eb533-140">Дополнительные сведения см. в разделе [как: добавление операторов трассировки tooApplication кода](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb533-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="eb533-141">Сохраните файл источника hello.</span><span class="sxs-lookup"><span data-stu-id="eb533-141">Save hello source file.</span></span>

