---
title: "aaaTroubleshooting с трассировкой событий | Документы Microsoft"
description: "Hello наиболее распространенных неполадок, возникающих при развертывании службы в Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Устранение распространенных проблем при развертывании служб в Azure Service Fabric
При запуске службы на компьютере разработчика, это просто toouse [средств отладки Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Для удаленных кластеров [отчеты о работоспособности](service-fabric-view-entities-aggregated-health.md) всегда являются toostart лучше всего. Здравствуйте, простой tooaccess способами, эти отчеты, с помощью PowerShell или [SFX](service-fabric-visualizing-your-cluster.md). В этой статье предполагается, что выполняется отладка удаленного кластера и иметь базовое понимание того, как toouse любой из этих средств.

## <a name="application-crash"></a>Сбой приложения
Hello» секция меньше целевой реплики или числа экземпляров» отчет — это означает, что произошло аварийное завершение службы. toofind, где произошло аварийное завершение службы занимает немного дополнительного изучения. Если служба масштабируется, незаменимыми будут тщательно продуманные трассировки.  Мы рекомендуем попробовать [диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md) для сбора этих трассировок и с помощью решения, такие как [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) для просмотра и поиска hello трассировок.

![Работоспособность секции SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Во время инициализации службы или субъекта
Все исключения до инициализации типа hello службы приведет к toocrash процесса hello. Эти типы сбоев журнал событий приложения hello будут показаны ошибки hello из службы.
Это наиболее распространенных исключения toosee hello до инициализации службы hello.

***System.IO.FileNotFoundException***

Эта ошибка часто является из-за зависимости между сборками toomissing. Проверьте свойство CopyLocal hello в Visual Studio или hello глобальный кэш сборок для узла hello.

***System.Runtime.InteropServices.COMException*** *в System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Это означает, что это имя типа зарегистрированную службу hello не соответствует hello манифест службы.

[Диагностика Azure](service-fabric-diagnostics-how-to-setup-wad.md) может быть автоматически настроенного tooupload hello журнал событий приложений для всех узлов.

### <a name="runasync-or-onactivateasync"></a>RunAsync() или OnActivateAsync()
Если происходит сбой hello во время инициализации hello или запущен зарегистрированную службу типа или субъект, hello исключение будет перехвачено Azure Service Fabric. Можно просмотреть эти от поставщиков EventSource hello, описанные в hello раздел «Дальнейшие действия».

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше о существующих видах диагностики, предоставляемых Service Fabric:

* [Диагностика Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Диагностика Reliable Services](service-fabric-reliable-services-diagnostics.md)

