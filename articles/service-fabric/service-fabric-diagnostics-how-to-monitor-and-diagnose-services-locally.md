---
title: "aaaDebug микрослужбами Azure в Windows | Документы Microsoft"
description: "Узнайте, как toomonitor и диагностики вашей службы, написанные с помощью Microsoft Azure Service Fabric на локальном компьютере разработчика."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Мониторинг и диагностика состояния служб в локальной среде разработки
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Мониторинг, обнаружение, диагностика и устранение неполадок позволяют toocontinue служб с минимальными нарушениями toohello пользователями. Хотя наблюдение и диагностику, важно в реальной производственной в развернутой среде, будут зависеть от эффективности hello заимствование аналогичной модели во время разработки tooensure служб, которыми они работают, при перемещении установки реальных tooa. Service Fabric упрощает диагностику tooimplement разработчики службы, можно легко работайте с одним компьютером локальная разработка настройки и настройки кластера реальных рабочих.

## <a name="event-tracing-for-windows"></a>Трассировка событий Windows
[Трассировка событий Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) — hello, рекомендуется использовать технологии для сообщения трассировки в Service Fabric. Преимущества использования трассировки событий Windows:

* **ETW работает быстро.** Технология разработана таким образом, что время выполнения кода практически не меняется.
* **Трассировка событий Windows одинаково работает в локальных средах разработки и в рабочем кластере.** Это означает, что у вас нет кода трассировки при готовности toodeploy toorewrite реальные кластера tooa кода.
* **Для внутренней трассировки системного кода Service Fabric также используется ETW.** Это позволяет tooview трассировок приложения перемежаться Service Fabric трассировки системы. Он также помогает toomore легко понять последовательностей hello и взаимосвязи между кодом приложения и события в базовой системе hello.
* **Нет встроенной поддержки в набор средств Visual Studio структуры службы tooview события трассировки событий Windows.** События трассировки событий Windows отображаются в hello представление события диагностики Visual Studio после Visual Studio неправильно настроена в Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Просмотр системных событий Service Fabric в Visual Studio
Service Fabric создает toohelp разработчикам понять, что произошло в платформе hello события трассировки событий Windows. Если это еще не сделано, загрузив и следуйте указаниям hello [создание первого приложения в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Эти сведения помогут вы получаете приложение работает с hello средство просмотра событий диагностики, показывающий hello сообщений трассировки.

1. Если Диагностика hello событий не отображается автоматически, они оказались toohello **представление** в Visual Studio, щелкните **другие окна** и затем **диагностические средства просмотра событий**.
2. Каждое событие получает информацию о стандартных метаданных, о том, что событие hello hello узла, приложения и службы, от которого поступил. Также можно фильтровать список hello событий с помощью hello **фильтровать события** поле hello верхней части окна событий hello. Например, вы можете выполнить фильтрацию по **имени узла** или **имени службы**. И при просмотре сведений о событии, можно также приостановить с помощью hello **приостановить** кнопку hello верхней части окна событий hello и возобновить позже без потери событий.
   
   ![Средство просмотра событий диагностики Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Добавьте свой код приложения toohello пользовательские трассировки
шаблоны проектов Service Fabric Visual Studio Hello содержится пример кода. Hello кода показано, как tooadd прикладной код трассировки событий Windows отслеживает где показано копирование в средстве просмотра событий Windows Visual Studio hello вместе с система трассировки из Service Fabric. Hello преимущество этого способа заключается в том tootraces автоматически добавляются метаданные hello Visual Studio диагностическое средство просмотра событий уже настроен toodisplay их.

Для проектов, созданных из hello **шаблонов службы** (без сохранения состояния или с отслеживанием состояния) точно так же, поиск hello `RunAsync` реализации:

1. Здравствуйте вызов слишком`ServiceEventSource.Current.ServiceMessage` в hello `RunAsync` метод является примером пользовательские трассировку ETW из кода приложения hello.
2. В hello **ServiceEventSource.cs** файл, вы обнаружите перегрузку для hello `ServiceEventSource.ServiceMessage` метод, который должен использоваться для событий с высокой частотой из-за причин tooperformance.

Для проектов, созданных из hello **шаблоны субъекта** (без сохранения состояния или с отслеживанием состояния):

1. Откройте hello **.cs «Имя_проекта»** файл where *ProjectName* является именем hello, выбранным для проекта Visual Studio.  
2. Поиск кода hello `ActorEventSource.Current.ActorMessage(this, "Doing Work");` в hello *DoWorkAsync* метод.  Это пример пользовательской точки трассировки ETW из кода приложения.  
3. В файле **ActorEventSource.cs**, вы обнаружите перегрузку для hello `ActorEventSource.ActorMessage` метод, который должен использоваться для событий с высокой частотой из-за причин tooperformance.

После добавления трассировка кода службы tooyour пользовательские трассировки событий Windows, можно построения, развертывания и запуска приложения hello снова toosee вашей события в hello диагностические средства просмотра событий. При отладке приложения hello с **F5**, hello диагностических событий в средстве просмотра автоматически.

## <a name="next-steps"></a>Дальнейшие действия
Hello же трассировка кода, добавленного tooyour приложения выше для локального диагностики будет работать со средствами, которые можно использовать tooview эти события при выполнении приложения в кластере Azure. Извлечь эти статьи, которые обсуждаются различные варианты hello средства hello и описывают, каким образом можно настроить их.

* [Каким образом toocollect ведет журнал диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Агрегирование и сбор событий с помощью EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

