---
title: "Обзор модели программирования aaaService структуры | Документы Microsoft"
description: "Service Fabric предлагает две платформы для построения служб: hello framework субъекта и платформа служб hello. Платформы отличаются уровнем сложности и контроля."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Общие сведения о модели программирования Service Fabric
Service Fabric предлагает несколько способов toowrite и управления службами. Службы можно выбрать hello toouse API-интерфейсы службы структуры tootake всеми преимуществами функции hello платформ и платформ приложений. Службы также могут представлять любую скомпилированную исполняемую программу, написанную на любом языке или с помощью любого кода, выполняемого в контейнере, размещенную в кластере Service Fabric.

## <a name="guest-executables"></a>Гостевые исполняемые файлы
[Гостевой исполняемый файл](service-fabric-deploy-existing-app.md) — это произвольный существующий исполняемый файл (написанный на любом языке), который может выполняться как служба в вашем приложении. Гость исполняемые файлы не вызывайте API пакета SDK для службы структуры hello напрямую. Однако они по-прежнему преимущества возможностей платформы hello предложения, такие как возможность обнаружения служб, пользовательские работоспособности и загрузки отчетов путем вызова REST API, предоставленным Service Fabric. Они также имеют поддержку полного жизненного цикла приложения.

Начните работать с такими приложениями, развернув свое первое [гостевое исполняемое приложение](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Контейнеры
По умолчанию Service Fabric развертывает и активирует службы как процессы. Service Fabric также позволяет развертывать службы в [контейнерах](service-fabric-containers-overview.md). Service Fabric поддерживает развертывание контейнеров Linux и контейнеров Windows на Windows Server 2016. Образы контейнеров может быть извлечено из любого контейнера репозитория и развернуты toohello машины. Существующие приложения можно развернуть в качестве гостя exectuables, без учета состояния или с отслеживанием состояния надежных служб Service Fabric или службы Reliable Actor в контейнерах и могут быть использованы смешанные службами в процессах и служб в контейнерах hello того же приложения.

[Дополнительные сведения о развертывании служб в контейнерах в Windows или Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Надежные службы
Надежные службы — это платформа недоступно для записи служб, которые интегрируются с платформы Service Fabric hello и преимущества hello полный набор возможностей платформы. Надежные службы предоставляют минимальный набор API-интерфейсы, позволяющие hello среда выполнения Service Fabric toomanage жизненного цикла hello служб и позволяющие toointeract вашей службы со средой выполнения hello. Платформа приложения Hello сводится к минимуму, предоставляя полный контроль над проектирования и реализации, а также может быть используется toohost все другие платформы приложений, таких как ASP.NET Core.

Надежные службы могут выполняться без сохранения состояния, аналогичную toomost службы платформ, например веб-серверов, в которых каждый экземпляр службы hello одинаковы и состояние сохраняется в внешнее решение, например базу данных Azure или хранилище таблиц Azure.

Надежные службы также может быть tooService с отслеживанием состояния, за исключением структуры, где сохраняется состояние непосредственно в службу hello себя с помощью надежного коллекций. Состояние становится высокодоступным за счет репликации и распределения путем секционирования, которыми автоматически управляет Service Fabric.

[Узнайте больше о надежных службах](service-fabric-reliable-services-introduction.md) или начните с [написания первой надежной службы](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Надежные субъекты
Построенный на базе надежной службы, hello Reliable Actor framework является исполняющую среду, реализующем шаблон Virtual Actor hello, на основе шаблона разработки hello субъекта. Hello Reliable Actor платформа использует независимые единицы вычислений и состояние с помощью однопоточного выполнения называется субъекты. Hello Reliable Actor framework предоставляет встроенные связи субъектами и предварительно заданное состояние конфигурации сохраняемости и масштабирования.

Как и сам службы Reliable Actor платформу приложения, построенные на надежные службы, полностью интегрирован с платформы Service Fabric hello и преимущества hello полный набор возможностей, предоставляемых платформой hello.

[Узнайте больше о надежных субъектах](service-fabric-reliable-actors-introduction.md) или начните с [написания первой службы надежного субъекта](service-fabric-reliable-actors-get-started.md).

## <a name="aspnet-core"></a>ASP.NET Core;
Service Fabric интегрируется с [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) для создания веб-службы и служб API, которые можно включать в приложения. 

[Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Дальнейшие действия
[Общие сведения о Service Fabric и контейнерах](service-fabric-containers-overview.md)

[Общие сведения о Reliable Services](service-fabric-reliable-services-introduction.md)

[Общие сведения о Reliable Services](service-fabric-reliable-actors-introduction.md)

[Service Fabric и ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)




