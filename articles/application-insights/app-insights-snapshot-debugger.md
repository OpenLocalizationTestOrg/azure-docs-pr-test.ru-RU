---
title: "aaaAzure отладчика моментального снимка аналитики приложений для приложений .NET | Документы Microsoft"
description: "Отладочные моментальные снимки автоматически собираются при порождении исключений в рабочих приложениях .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Отладочные моментальные снимки для исключений в приложениях .NET

При возникновении исключения, можно автоматически собирать отладочный моментальный снимок из работающего веб-приложения. снимок Hello отображает состояние hello исходного кода и переменные в hello момент hello исключение создано исключение. Hello отладчик моментальных снимков (Предварительная версия) в [Azure Application Insights](app-insights-overview.md) отслеживает телеметрии исключения из веб-приложения. Собирает моментальные снимки на свои исключения, создающие top, чтобы получить сведения hello необходимы toodiagnose проблем в рабочей среде. Включить hello [пакет NuGet сборщика данных моментального снимка](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) в приложении и при необходимости настроить параметры сбора в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Снимки появятся на [исключения](app-insights-asp-net-exceptions.md) на портале Application Insights hello.

Можно просмотреть моментальные снимки отладки в стеке вызовов hello портала toosee hello и просматривать переменные в каждом кадре стека вызовов. более широкие возможности отладки для работы с исходным кодом, откройте моментальные снимки с помощью Visual Studio Enterprise 2017 г., tooget [загрузка расширения отладчика моментального снимка hello для Visual Studio](https://aka.ms/snapshotdebugger).

Коллекция моментальных снимков доступна для:
* .NET Framework и приложений ASP.NET выполняющихся с помощью .NET Framework 4.5 или более поздней версии.
* .NET Core 2.0 и приложений ASP.NET Core 2.0 под управлением Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Настройка сбора моментальных снимков для приложений

1. [Включите Application Insights в веб-приложении](app-insights-asp-net.md), если вы еще не сделали это.

2. Включить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении. 

3. Просмотрите параметры по умолчанию hello, hello пакет добавлен слишком[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Моментальные снимки собираются только на исключения, которые выводятся tooApplication аналитики. В некоторых случаях (например, предыдущие версии платформы .NET hello) может потребоваться слишком[настроить коллекцию исключений](app-insights-asp-net-exceptions.md#exceptions) toosee исключения с моментальными снимками в портале hello.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Настройка сбора моментальных снимков для приложений ASP.NET Core 2.0

1. [Включите Application Insights в веб-приложении ASP.NET Core](app-insights-asp-net-core.md), если вы еще не сделали это.

2. Включить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении.

3. Изменение hello `ConfigureServices` метод в вашем приложении `Startup` класса процессора телеметрии tooadd hello моментального снимка сборщика. Hello кода, который следует добавить зависит от указанной версии hello пакет Microsoft.ApplicationInsights.ASPNETCore NuGet hello.

   Для Microsoft.ApplicationInsights.AspNetCore 2.1.0 добавьте:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Для Microsoft.ApplicationInsights.AspNetCore 2.1.1 добавьте:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Настройка сбора моментальных снимков для других приложений .NET

1. Если приложение уже не инструментированы с помощью Application Insights, начните с [Включение Application Insights и ключ инструментирования hello параметр](app-insights-windows-desktop.md).

2. Добавить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении.

3. Моментальные снимки собираются только на исключения, которые выводятся tooApplication аналитики. Может потребоваться toomodify tooreport вашего кода их. код обработки исключений Hello зависит от структуры приложения hello, но пример приведен ниже:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Предоставление разрешений

Владельцы hello подписки Azure можно проверить и моментальные снимки. Другие пользователи должны иметь разрешение предоставленное владельцем.

toogrant разрешений, назначьте hello `Application Insights Snapshot Debugger` toousers роли, который будет проверять моментальные снимки. Этой роли могут назначаться tooindividual пользователи или группы, ответственные за подписку для hello целевой ресурс Application Insights или его группы ресурсов или подписки.

1. Откройте колонку hello управления доступа (IAM).
1. Щелкните Здравствуйте, "+" Кнопка "Добавить".
1. Выберите отладчик моментального снимка аналитики приложения из раскрывающегося списка ролей hello.
1. Поиск и введите имя пользователя tooadd hello.
1. Щелкните hello tooadd кнопки Save hello роли toohello пользователя.


[!IMPORTANT]
    Моментальные снимки могут содержать личные и другие конфиденциальные данные в значениях переменных и параметров.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Отладка моментальные снимки на портале Application Insights hello

Если моментальный снимок доступен для данного исключения или проблемный идентификатор **открыть снимок отладки** кнопка на hello [исключение](app-insights-asp-net-exceptions.md) на портале Application Insights hello.

![Кнопка "Open Debug Snapshot" (Открыть отладочный моментальный снимок) для исключения](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

В hello снимок отладки отображается стек вызовов и панель «переменные». При выборе кадров вызова hello стека в панели стека вызова hello, можно просматривать локальные переменные и параметры для этой функции вызова в панель «переменные» hello.

![Представление отладки моментального снимка в портале hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Моментальные снимки могут содержать конфиденциальные сведения и по умолчанию не отображаются. моментальные снимки tooview, необходимо иметь hello `Application Insights Snapshot Debugger` tooyou ролью.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Отладка моментальных снимков с помощью Visual Studio 2017 Enterprise
1. Щелкните hello **загрузить моментальный снимок** toodownload кнопку `.diagsession` файл, который можно открыть в Visual Studio Enterprise 2017 г. 

2. tooopen hello `.diagsession` файл, сначала необходимо выполнить [загрузить и установить расширения hello отладчика моментальных снимков для Visual Studio](https://aka.ms/snapshotdebugger).

3. После открытия файла моментального снимка hello, откроется страница отладки минидампа hello в Visual Studio. Нажмите кнопку **отладки управляемого кода** toostart отладки hello моментального снимка. моментальный снимок Hello открывает toohello строку кода, где hello возникло исключение, чтобы выполнить отладку hello текущему состоянию процесса hello.

    ![Просмотр отладочного моментального снимка в Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

загруженный моментальный снимок Hello содержит все файлы символов, которые найдены на сервер веб-приложения. Эти файлы символов, необходимых tooassociate данных моментального снимка с исходным кодом. Для приложений служб приложений легко и убедиться, что развертывание символ tooenable при публикации веб-приложения.

## <a name="how-snapshots-work"></a>Как работают моментальные снимки

При запуске приложения создается отдельный процесс передачи моментальных снимков, отслеживающий запросы на создание моментальных снимков для вашего приложения. При запросе моментального снимка около 10 минут too20 теневая копия выполнения процесса hello производится. процесс теневого Hello затем анализируется и моментальный снимок создается прерывая toorun основной процесс hello и обслуживать toousers трафика. Hello моментального снимка является то отправленного tooApplication аналитики вместе с любой соответствующих символов (.pdb) файлы, необходимые tooview hello моментального снимка.

## <a name="current-limitations"></a>Текущие ограничения

### <a name="publish-symbols"></a>Публикация символов
Hello отладчик моментальных снимков требуются файлы символов на hello рабочей toodecode переменные сервера и tooprovide возможности отладки в Visual Studio. символы для сборки выпуска публикует Hello 15,2 выпуска Visual Studio 2017 г. по умолчанию при публикации tooApp службы. В предыдущих версиях требуются следующие hello tooadd профиль публикации tooyour строки `.pubxml` так, чтобы символы публикуются в режиме выпуска:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Для вычисления Azure и других типов, убедитесь, что файлы символов hello в hello папке .dll основного приложения hello (как правило, `wwwroot/bin`) и доступные в текущем пути hello.

### <a name="optimized-builds"></a>Оптимизированные сборки
В некоторых случаях нельзя просмотреть локальные переменные в сборках выпуска из-за оптимизации, которые применяются во время сборки hello.

## <a name="troubleshooting"></a>Устранение неполадок

Эти советы помочь при устранении проблем с hello отладчик моментального снимка.

### <a name="verify-hello-instrumentation-key"></a>Проверьте ключ инструментирования hello

Убедитесь, что вы используете ключ правильный инструментирования hello опубликованного приложения. Как правило Application Insights считывает hello ключ инструментирования из файла ApplicationInsights.config hello. Убедитесь, что значение hello hello таким же как ключ инструментирования hello для ресурса Application Insights hello, который представлен в портал hello.

### <a name="check-hello-uploader-logs"></a>Проверьте журналы средства отправки hello

После создания моментального снимка на диске создается файл минидампа (.dmp). Процесс передачи отдельных принимает этот файл минидампа и передает его, а также любые связанные PDB-файлы tooApplication отладчик моментального снимка аналитики хранилища. После успешной загрузки минидампа hello удаляется с диска. файлы журнала Hello для передачи минидампа hello сохраняются на диске. В среде службы приложений эти журналы можно найти в `D:\Home\LogFiles\Uploader_*.log`. Kudu управления использовать hello сайт для служб приложений toofind файлов журналов.

1. Откройте приложение службы приложений в hello портал Azure.

2. Выберите hello **дополнительные средства** колонке или выполните поиск **Kudu**.
3. Щелкните **Переход**.
4. В hello **консоли отладки** раскрывающегося списка и выберите **CMD**.
5. Щелкните **LogFiles**.

Вы увидите хотя бы один файл с именем, начинающимся с `Uploader_` и расширением `.log`. Щелкните соответствующий значок toodownload hello все файлы журналов, или открыть их в браузере.
Имя файла Hello включает имя машины hello. Если экземпляр службы приложений размещен на нескольких компьютерах, для каждого компьютера существуют отдельные файлы журналов. Когда средства отправки hello обнаруживает новый файл минидампа, она заносится в файл журнала hello. Ниже приведен пример успешной отправки:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

В предыдущем примере hello является ключ инструментирования hello `c12a605e73c44346a984e00000000000`. Это значение должно соответствовать hello ключ инструментирования для вашего приложения.
Hello минидампа связан с помощью моментального снимка с Идентификатором hello `139e411a23934dc0b9ea08a626db16c5`. Вы можете использовать этот идентификатор более поздней версии toolocate hello связанные данные телеметрии исключения из приложения аналитика Analytics.

средства отправки Hello проверяет наличие новых PDB-файлы примерно один раз каждые 15 минут. Ниже приведен пример:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Для приложений, которые являются _не_ размещенных в службе приложений hello средства отправки записываются hello же папке, что мини-дампов hello: `%TEMP%\Dumps\<ikey>` (где `<ikey>` ваш ключ инструментирования).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Используйте Application Insights поиска toofind исключения с помощью моментальных снимков

При создании моментального снимка hello исключения обозначен цифрой идентификатора моментального снимка. Когда телеметрии исключения hello обнаруженную tooApplication аналитики, этот идентификатор моментального снимка включается в качестве пользовательского свойства. С помощью поиска колонке hello в Application Insights, можно найти все данные телеметрии с hello `ai.snapshot.id` пользовательское свойство.

1. Обзор tooyour ресурс Application Insights в hello портал Azure.
2. Щелкните **Search**(Поиск).
3. Тип `ai.snapshot.id` в hello текстовое поле поиска и нажмите клавишу ВВОД.

![Поиск телеметрии с идентификатор снимка в портале hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Если этот поиск не дал результатов, без моментальных снимков были обнаруженную tooApplication аналитики для приложения hello выбранного диапазона времени.

toosearch для идентификатора конкретного моментального снимка из журналов средства отправки hello, введите этот идентификатор в поле поиска hello. Если не удается найти данные телеметрии для моментального снимка, который был отправлен, выполните следующие действия:

1. Проверьте, что вы рассматриваете возможность hello ресурса Application Insights, проверяя ключ инструментирования hello.

2. С помощью hello меткам hello средства отправки журнала, настройте этот диапазон фильтр поиска toocover hello hello диапазон времени.

Если исключение с таким Идентификатором моментальных снимков по-прежнему отсутствует, телеметрии исключения hello не обнаруженную tooApplication аналитики. Это происходит в случае сбоя приложения после потребовалось hello моментального снимка, но прежде чем они отчет hello телеметрии исключений. В этом случае проверьте hello, приложение будет зарегистрировано в `Diagnose and solve problems` toosee, если возникли непредвиденные перезагрузки или необработанные исключения.

## <a name="next-steps"></a>Дальнейшие действия

* [Установить в коде snappoints](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget моментальные снимки, не дожидаясь исключение.
* [Диагностика исключения в веб-приложения](app-insights-asp-net-exceptions.md) объясняет, как toomake дополнительные исключения видимым tooApplication аналитики. 
* В статье [Интеллектуальное обнаружение в Application Insights](app-insights-proactive-diagnostics.md) описывается автоматическое обнаружение аномалий производительности.
