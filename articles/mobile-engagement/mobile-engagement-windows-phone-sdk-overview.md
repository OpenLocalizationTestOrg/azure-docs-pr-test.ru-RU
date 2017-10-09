---
title: "Обзор пакета SDK для Silverlight Windows Phone Mobile Engagement aaaAzure | Документы Microsoft"
description: "Общие сведения о Windows Phone Silverlight и пакет SDK для Azure Mobile Engagement hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Общие сведения о пакете SDK для Windows Phone Silverlight для Служб мобильного взаимодействия Azure
Начните здесь tooget hello сведения о том, как toointegrate Azure Mobile Engagement в приложениях Windows Phone Silverlight. Если вы хотите toogive она try прежде всего убедитесь, можно выполнить наши [учебника 15 минут](mobile-engagement-windows-phone-get-started.md).

Нажмите кнопку toosee hello [содержимого пакета SDK](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Процедуры по интеграции
1. Начните здесь: [как toointegrate Mobile Engagement в приложения Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Для получения уведомлений: [как toointegrate Reach (уведомлений) в приложении Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Тег план реализации: [как toouse hello дополнительные теги API в приложения Windows Phone Silverlight мобильного охвата](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Заметки о выпуске
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Часть hello *MicrosoftAzure.MobileEngagement* пакет Nuget **v3.4.1**

* Улучшение стабильности.

Для более ранней версии см. в разделе hello [завершения заметки о выпуске](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Процедуры обновления
Если уже имеется встроенный более старой версии нашего пакета SDK в приложение, у вас есть следующие точки, при обновлении hello SDK hello tooconsider.

Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello. См. полный hello [обновление процедуры](mobile-engagement-windows-phone-upgrade-procedure.md). Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.

### <a name="from-200-too330"></a>Из 2.0.0 too3.3.0
#### <a name="test-logs"></a>Журналы тестирования
Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются. toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Обновление предыдущих версий
См. статью [Процедуры обновления SDK универсальных приложений для Windows](mobile-engagement-windows-phone-upgrade-procedure.md).

