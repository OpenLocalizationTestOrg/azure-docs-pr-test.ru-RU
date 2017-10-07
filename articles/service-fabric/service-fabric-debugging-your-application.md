---
title: "aaaDebug приложения в Visual Studio | Документы Microsoft"
description: "Улучшить hello надежность и производительность служб по разработке и отладке их в кластере локальной разработки в Visual Studio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Отладка приложения Service Fabric с помощью Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio и CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse и Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Отладка локального приложения Service Fabric
Вы можете сэкономить время и деньги, развернув приложение Azure Service Fabric и выполнив его отладку в кластере для разработки, состоящем из локальных компьютеров. Visual Studio 2017 г. или Visual Studio 2015 можно развернуть локальный кластер hello приложения toohello и автоматически подключить hello отладчик tooall экземпляров приложения.

1. Запуск разработки локального кластера с помощью инструкции hello в [Настройка среды разработки Service Fabric](service-fabric-get-started.md).
2. Нажмите клавишу **F5** или выберите в меню **Отладка** > **Начать отладку**.
   
    ![Запуск отладки приложения][startdebugging]
3. Установите точки останова в коде и пошаговое выполнение приложения hello, выбирая команды в hello **отладки** меню.
   
   > [!NOTE]
   > Visual Studio подключает tooall экземпляры приложения. При пошаговом выполнении кода разные процессы могут одновременно достигать точек останова. Это приводит к возникновению параллельных сеансов. Попробуйте отключить hello точки останова после их работе, сделав условного на идентификатор потока hello каждой точке останова или с помощью событий диагностики.
   > 
   > 
4. Hello **события диагностики** автоматически будет открыто окно, чтобы можно было просматривать диагностические события в режиме реального времени.
   
    ![Просмотр событий диагностики в режиме реального времени][diagnosticevents]
5. Можно также открыть hello **события диагностики** окна в Cloud Explorer.  В разделе **Service Fabric** щелкните любой узел правой кнопкой мыши и выберите пункт **Показать потоковую передачу трассировок**.
   
    ![Привет открыть окно событий диагностики][viewdiagnosticevents]
   
    Если требуется toofilter трассировок tooa определенной службы или приложения, просто включите потоковой передачи трассировки во время этой конкретной службы или приложения.
6. события диагностики Hello можно увидеть в hello автоматически создается **ServiceEventSource.cs** файла и вызова из кода приложения.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Hello **события диагностики** окно поддерживает фильтрацию, приостановка и проверка события в режиме реального времени.  Фильтр Hello — простой поиск строки сообщения hello события, включая его содержимое.
   
    ![Фильтрация, приостановка, возобновление и проверка событий в реальном времени][diagnosticeventsactions]
8. Отладка служб аналогична отладке приложений. Обычно для простой отладки точки останова задаются в Visual Studio. Несмотря на то, что надежные коллекции реплицируются на нескольких узлах, они все равно реализуют интерфейс IEnumerable. Это означает, что можно использовать hello Просмотр результатов в Visual Studio во время отладки toosee хранятся внутри. Просто задайте точку останова в любом месте своего кода.
   
    ![Запуск отладки приложения][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Отладка удаленного приложения Service Fabric
Если приложения Service Fabric запущены в кластере Service Fabric в Azure,-можно tooremotely отладки их непосредственно из Visual Studio.

> [!NOTE]
> функции Hello требуется [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) и [пакет Azure SDK для .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Удаленная отладка предназначена для сценариев разработки и тестирования и не toobe, используемый в производственной среде, из-за hello влияние на выполнение приложений hello.
> 
> 

1. Перехода кластера tooyour в **Cloud Explorer**, щелкните правой кнопкой мыши и выберите **Включение отладки**
   
    ![Включение удаленной отладки][enableremotedebugging]
   
    Это запускается процесс hello включения hello удаленной отладки расширения на узлы кластера, а также необходимые конфигурации сети.
2. Щелкните правой кнопкой мыши узел кластера hello в **Cloud Explorer**и выберите **присоединить отладчик**
   
    ![Подключить отладчик][attachdebugger]
3. В hello **присоединения tooprocess** диалоговое окно, выберите процесс hello toodebug и нажмите кнопку **присоединения**
   
    ![Выбор процесса][chooseprocess]
   
    Имя Hello hello процесса нужно tooattach для, равно hello имя службы имя сборки проекта.
   
    узлы tooall hello процесс присоединения отладчика Hello.
   
   * В случае hello, где при отладке службы без отслеживания состояния все экземпляры службы hello на всех узлах являются частью сеанса отладки hello.
   * При отладке службы с отслеживанием состояния hello только первичная реплика любого раздела будет активна и поэтому перехваченного отладчиком hello. Если первичная реплика hello перемещается во время сеанса отладки hello, hello обработки этой реплики будет по-прежнему входить hello сеанса отладки.
   * В порядке tooonly catch секций или экземпляров данной службы можно использовать условные точки останова tooonly разрыв определенный раздел или экземпляр.
     
     ![Условная точка останова][conditionalbreakpoint]
     
     > [!NOTE]
     > В настоящее время мы не поддерживают отладку кластера Service Fabric с несколькими экземплярами hello же имя исполняемого файла службы.
     > 
     > 
4. После завершения отладки приложения hello расширение удаленной отладки можно отключить, щелкнув правой кнопкой мыши кластер hello в **Cloud Explorer** и выберите **Запретить отладку**
   
    ![Отключение удаленной отладки][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Потоковая передача трассировок из удаленного узла кластера
Вы также являются трассировки может toostream непосредственно из удаленного кластера узла tooVisual Studio. Эта функция позволяет события трассировки ETW toostream, полученных на узле кластера Service Fabric.

> [!NOTE]
> Компоненту требуется [пакет SDK 2.0 для Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) и [пакет SDK Azure для .NET 2.9](https://azure.microsoft.com/downloads/).
> Эта функция поддерживает только кластеры на платформе Azure.
> 
> 

<!-- -->
> [!WARNING]
> Потоковая передача трассировок предназначена для сценариев разработки и тестирования и не toobe, используемый в производственной среде, из-за hello влияние на выполнение приложений hello.
> В рабочем сценарии следует применять пересылку событий с помощью средств диагностики Azure.
> 
> 

1. Перехода кластера tooyour в **Cloud Explorer**, щелкните правой кнопкой мыши и выберите **Включение трассировки потоковой передачи**
   
    ![Включение трассировки удаленной потоковой передачи][enablestreamingtraces]
   
    Это запускается процесс hello включения hello потоковой передачи расширение трассировки на узлы кластера, а также необходимые конфигурации сети.
2. Разверните hello **узлы** элемент в **Cloud Explorer**, щелкните правой кнопкой мыши узел hello toostream трассировок из и задайте **представление трассировки потоковой передачи**
   
    ![Просмотр трассировки удаленной потоковой передачи][viewremotestreamingtraces]
   
    Повторите шаг 2 для столько требуется toosee трассировок из узлов. Потоковая передача каждого узла будет отображаться в отдельном окне.
   
    Теперь вы находитесь может toosee hello трассировки, относящиеся к Service Fabric и служб. Если вы хотите toofilter hello события tooonly отображение конкретного приложения, просто введите имя hello приложения hello в фильтре hello.
   
    ![Просмотр трассировки потоковой передачи][viewingstreamingtraces]
3. После завершения трассировки потоковой передачи из кластера, можно отключить трассировку удаленной потоковой передачи, щелкните правой кнопкой мыши кластер hello в **Cloud Explorer** и выберите **отключить потоковую передачу трассировок**
   
    ![Отключение трассировки удаленной потоковой передачи][disablestreamingtraces]

## <a name="next-steps"></a>Дальнейшие действия
* [Проверка службы Service Fabric](service-fabric-testability-overview.md)
* [Управление приложениями Service Fabric в Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
