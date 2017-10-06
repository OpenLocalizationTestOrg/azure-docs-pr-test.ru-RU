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
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Трассировка потока hello облачные службы приложения с помощью системы диагностики Azure
Трассировка — это способ для вас toomonitor hello выполнения приложения, пока она запущена. Можно использовать hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), и [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) классы toorecord сведения об ошибках и выполнение приложения в журналы, текстовые файлы или другие устройства для последующего анализа. Дополнительные сведения о трассировке см. в статье [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx) (Трассировка и инструментирование приложений).

## <a name="use-trace-statements-and-trace-switches"></a>Использование трассировочных операторов и переключателей
Реализуйте трассировку в приложении облачные службы, добавив hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello конфигурации приложения и внесения вызывает tooSystem.Diagnostics.Trace или System.Diagnostics.Debug в вашей код приложения. Использование файла конфигурации hello *app.config* для рабочих ролей и hello *web.config* для веб-ролей. При создании новой размещенной службы с помощью шаблона Visual Studio автоматически добавляется проект toohello диагностики Azure и hello DiagnosticMonitorTraceListener добавляется toohello соответствующий файл конфигурации для hello ролей, которые вы добавляете.

Сведения о размещении операторов трассировки см. в разделе [как: добавление операторов трассировки tooApplication кода](https://msdn.microsoft.com/library/zd83saa2.aspx).

Процессом и масштабом трассировки можно управлять. Для этого добавьте в код [переключатели трассировки](https://msdn.microsoft.com/library/3at424ac.aspx). Это позволяет отслеживать состояние приложения в производственной среде hello. Это особенно важно в бизнес-приложениях, которые используют различные компоненты, выполняющиеся на нескольких компьютерах. Дополнительные сведения см. в статье [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx) (Настройка переключателей трассировки).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Настройте прослушиватель трассировки hello в приложении Azure
Trace, Debug и TraceSource, требуют настройки toocollect «прослушиватели» и сообщения hello записей, которые были отправлены. Прослушиватели собирают, хранят и перенаправляют сообщения трассировки. Они направлять hello трассировки вывода tooan соответствующему целевому объекту, например журнал, окно или текстовый файл. Диагностика Azure использует hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) класса.

Перед выполнением процедуры hello необходимо инициализировать монитор диагностики Azure hello. toodo это, см. в разделе [включение диагностики в Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Обратите внимание, что при использовании hello шаблонов, предоставляемых средой Visual Studio, конфигурации hello hello прослушивателя добавляется автоматически.

### <a name="add-a-trace-listener"></a>Добавление прослушивателя трассировки
1. Откройте файл web.config или app.config hello для вашей роли.
2. Добавьте следующие toohello файл кода hello. Измените hello атрибут toouse hello версии номер версии hello сборки, на которую имеются ссылки. версия сборки Hello не обязательно изменяет с каждым выпуском пакета Azure SDK только при наличии обновлений tooit.
   
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
   > Убедитесь, что у вас есть toohello ссылки проекта Microsoft.WindowsAzure.Diagnostics сборки. Номер версии обновления hello в xml hello выше версии hello toomatch hello связанной сборки Microsoft.WindowsAzure.Diagnostics.
   > 
   > 
3. Сохраните файл конфигурации hello.

Дополнительные сведения о прослушивателях см. [здесь](https://msdn.microsoft.com/library/4y5y10s7.aspx).

После завершения tooadd hello hello действия прослушивателя, можно добавить код tooyour операторы трассировки.

### <a name="tooadd-trace-statement-tooyour-code"></a>Инструкция tooyour tooadd трассировки кода
1. Откройте исходный файл приложения. Например, hello <RoleName>CS-файл для hello рабочей роли или веб-роли.
2. Добавьте следующее hello с помощью инструкции, если он уже не был добавлен:
    ```
        using System.Diagnostics;
    ```
3. Добавьте инструкции Trace место toocapture сведения о состоянии приложения hello. Можно использовать различные методы tooformat hello выходные данные операторов трассировки hello. Дополнительные сведения см. в разделе [как: добавление операторов трассировки tooApplication кода](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Сохраните файл источника hello.

