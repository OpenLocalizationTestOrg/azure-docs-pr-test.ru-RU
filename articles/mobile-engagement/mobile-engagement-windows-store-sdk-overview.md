---
title: "aaaAzure универсальной интеграции пакета SDK Mobile Engagement Windows | Документы Microsoft"
description: "Интеграция универсальных приложений для Windows с пакетом SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Интеграция пакета SDK универсальных приложений для Windows для Служб мобильного взаимодействия Azure
В этом документе приводится описание всех hello интеграции и настройки параметров для универсальной SDK Azure Mobile Engagement Windows hello.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступить к этому учебнику, необходимо изучить [наш 15-минутный учебник](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Дополнительные функции
### <a name="reporting-features"></a>Функции отчетов
Можно добавить такие функции:

1. [дополнительные параметры отчетов;](mobile-engagement-windows-store-advanced-reporting.md)
2. [Расширенные параметры конфигурации](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Уведомления
[Как toointegrate Reach (уведомлений) в приложении Windows Universal.](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Реализация плана добавления тегов:
[Как toouse hello advanced мобильного охвата, добавление тегов API в приложении Windows Universal.](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Заметки о выпуске
### <a name="341-11032016"></a>3.4.1 (03.11.2016)

* Улучшение стабильности.

Для более ранних версий, в разделе hello [завершения заметки о выпуске](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Процедуры обновления
Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.

Если вы пропустили несколько версий пакета SDK для hello, возможно toofollow несколько процедур. См. полный hello [обновление процедуры](mobile-engagement-windows-store-upgrade-procedure.md). Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.

### <a name="from-330-too340"></a>Из 3.3.0 too3.4.0
#### <a name="test-logs"></a>Журналы тестирования
Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются. toocustomize обновить свойство hello `EngagementAgent.Instance.TestLogEnabled` tooone hello значений, доступных из hello `EngagementTestLogLevel` перечисления, например:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Ресурсы
Улучшена Hello Reach наложения. Он является частью ресурсы пакета SDK NuGet hello.

При обновлении toohello новую версию пакета SDK для hello, можно выбрать, следует tookeep ли существующие файлы из hello наложения папки ресурсов или нет.

* Если предыдущих наложения hello работает для вас или интеграции hello `WebView` элементы вручную, можно указать tookeep на выход из файлов, она по-прежнему будет работать.
* новый наложения toohello tooupdate, hello замены всего `overlay` папку из ресурсов с hello новый из пакета SDK для hello (приложений UWP: после обновления hello можно получить hello наложения папку % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> С помощью нового наложения hello перезаписывает все настройки, произведенные в предыдущей версии hello.
> 
> 

### <a name="upgrade-from-older-versions"></a>Обновление предыдущих версий
См. статью [Процедуры обновления SDK универсальных приложений для Windows](mobile-engagement-windows-store-upgrade-procedure.md).

