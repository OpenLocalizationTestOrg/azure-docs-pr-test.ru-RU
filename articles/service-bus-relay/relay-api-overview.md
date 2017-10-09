---
title: "Обзор интерфейса API ретрансляции aaaAzure | Документы Microsoft"
description: "Обзор доступных интерфейсов API ретранслятора Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>Доступные интерфейсы API ретранслятора

## <a name="runtime-apis"></a>API среды выполнения

Hello следующей таблице перечислены все клиенты в настоящее время доступна ретрансляции среды выполнения.

Hello [дополнительной информацией](#additional-information) раздел содержит дополнительные сведения о состоянии hello каждой библиотеки времени выполнения.

| Язык или платформа | Доступная функция | Пакет клиента | Репозиторий |
| --- | --- | --- | --- |
| .NET Standard | через гибридные подключения | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | Ретранслятор WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | Недоступно |
| Узел | через гибридные подключения | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Дополнительная информация

#### <a name="net"></a>.NET
экосистема Hello .NET имеет несколько сред выполнения, таким образом, существует несколько библиотек .NET для концентраторов событий. Hello .NET стандартной библиотеки могут выполняться с помощью .NET Core или hello .NET Framework, пока hello библиотеки .NET Framework может выполняться только в среде .NET Framework. Дополнительные сведения о версиях платформы .NET Framework см. в разделе [Версии платформ](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:
* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Вопросы и ответы по ретранслятору](relay-faq.md)