---
title: "Обзор интерфейса API концентраторов событий aaaAzure | Документы Microsoft"
description: "Обзор доступных интерфейсов API концентраторов событий Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>Доступные интерфейсы API концентраторов событий

## <a name="runtime-apis"></a>API среды выполнения

Hello ниже приводится описание всех доступных в данный момент клиентов концентраторов событий Azure времени выполнения. Хотя некоторые из этих библиотек также содержат функциональные возможности ограниченные возможности управления, есть также [определенных библиотек](#management-apis) выделенного toomanagement операций. основной темой Hello эти библиотеки является toosend и получение сообщений из концентратора событий.

В разделе [дополнительной информацией](#additional-information) для получения дополнительных сведений о hello текущее состояние каждого библиотеки времени выполнения.

| Язык или платформа | Пакет клиента | Пакет EventProcessorHost | Репозиторий |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | Недоступно |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Узел | [NPM](https://www.npmjs.com/package/azure-event-hubs) | Недоступно | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | Недоступно | Недоступно | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Дополнительная информация

#### <a name="net"></a>.NET
экосистема Hello .NET имеет несколько сред выполнения, таким образом, существует несколько библиотек .NET для концентраторов событий. Hello .NET стандартной библиотеки могут выполняться с помощью .NET Core или hello .NET Framework, пока hello библиотеки .NET Framework может выполняться только в среде .NET Framework. Дополнительные сведения о версиях платформы .NET Framework см. в разделе [Версии платформ](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Узел

Библиотека Node.js Hello в настоящее время находится в предварительной версии и поддерживаются как части проекта с сотрудниками корпорации Майкрософт и внешних участников. Все добавляемые материалы, включая исходный код, принимаются и проверяются.

## <a name="management-apis"></a>API управления

Hello ниже приведен список всех доступных в настоящее время управления определенных библиотек. Ни один из этих библиотек содержат операций среды выполнения и являются единственной целью hello управления сущностями концентраторов событий.

| Язык или платформа | Пакет управления | Репозиторий |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)