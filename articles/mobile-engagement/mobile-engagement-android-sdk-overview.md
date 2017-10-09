---
title: "aaaAndroid интеграции пакета SDK для Azure Mobile Engagement"
description: "Описывает способ toointegrate Azure Mobile Engagement SDK в приложения Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Интеграция пакета SDK для Служб мобильного взаимодействия Azure с Android
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

В этом документе приводится описание всех hello интеграции и настройки параметров для Azure Mobile Engagement Android SDK.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Дополнительные функции
### <a name="reporting-features"></a>Функции отчетов
Можно добавить такие функции:

1. [дополнительные параметры отчетов;](mobile-engagement-android-advanced-reporting.md)
2. [параметры отчетов о местонахождении;](mobile-engagement-android-location-reporting.md)
3. [дополнительные параметры конфигурации.](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Уведомления:
[Как toointegrate Reach (уведомлений) в приложении Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [как tooIntegrate GCM с мобильного охвата](mobile-engagement-android-gcm-integrate.md)
2. Обмен сообщениями устройства Amazon (ADM): [как tooIntegrate ADM с мобильного охвата](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Реализация плана добавления тегов:
[Как toouse hello advanced мобильного охвата, добавление тегов API в приложении Android](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Заметки о выпуске

### <a name="431-07172017"></a>4.3.1 (17.07.2017)
* Исключена аварийного завершения работы, которая могла происходить редко, при вызове `EngagementAgentUtils.isInDedicatedEngagementProcess`, который также используется для hello `EngagementApplication` класса.

### <a name="430-06272017"></a>4.3.0 (27.06.2017)
* 8 Поддержка Android (предыдущие версии hello SDK не будет работать в Android 8).
* Удалена зависимость от библиотеки поддержки.
* Удален класс `EngagementFragmentActivity`.
* Из-за слишком[ограничения выполнения фоновой](https://developer.android.com/preview/features/background.html) в Android 8 журналы в фоновом режиме может быть отложен до hello пользователь взаимодействует с устройством hello, это повлияет на кампании Push **доставлено** и **Системное уведомление выводится** статистики задерживается, если устройство hello находится в спящем режиме (hello уведомление будет отображаться, будет кольца и компакт-дисков в реальном времени без проблем).
* Из-за слишком[ограничения расположения фона](https://developer.android.com/preview/features/background-location-limits.html), расположение hello реального времени в фоновом режиме не будет часто обновляться в Android 8.

Для всех версий см. в разделе hello [завершения заметки о выпуске](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Процедуры обновления
Если вы уже интегрировали более старую версию нашего пакета SDK в приложение, ознакомьтесь с разделом [Процедуры обновления](mobile-engagement-android-upgrade-procedure.md).

