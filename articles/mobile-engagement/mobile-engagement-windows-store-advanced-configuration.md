---
title: "aaaAdvanced конфигурации для универсальных приложений Engagement пакета SDK для Windows"
description: "Параметры расширенной конфигурации Служб мобильного взаимодействия Azure при использовании с универсальными приложениями для Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Расширенная конфигурация пакета SDK службы Engagement для универсальных приложений для Windows
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Эта процедура описывает, как tooconfigure различные параметры конфигурации для приложения Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Расширенная конфигурация
### <a name="disable-automatic-crash-reporting"></a>Отключение автоматического создания отчетов о сбоях
Можно отключить hello аварийного завершения автоматического компонент рвением отчетов. Тогда при возникновении необработанного исключения служба Engagement не будет выполнять никаких действий.

> [!WARNING]
> Если отключить эту функцию, то при возникновении необработанного аварийного завершения приложения Engagement не отправляет аварийного завершения hello **AND** не приводит к закрытию сеанса hello и заданий.
> 
> 

автоматического создания отчетов, о сбоях toodisable настроить конфигурацию, в зависимости от того, она была объявлена как hello:

#### <a name="from-engagementconfigurationxml-file"></a>Из файла `EngagementConfiguration.xml`
Отчет набора аварийное завершение работы слишком`false` между `<reportCrash>` и `</reportCrash>` тегов.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Из объекта `EngagementConfiguration` во время выполнения
Задать toofalse сбоя отчетов с помощью объекта EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Отключение отчетов в реальном времени
По умолчанию hello Engagement службы отчетов входит в режиме реального времени. Если приложение сообщает журналы часто, это лучше toobuffer hello журналы и tooreport их все за один раз на основе рабочее время. Это называется пакетным режимом.

toodo таким образом, необходимо вызвать метод hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello аргумент представляет собой значение в **миллисекунд**. Каждый раз, когда требуется, чтобы в режиме реального времени ведения журнала hello tooreactivate, вызовите метод hello без какого-либо параметра или со значением hello 0.

Пакетный режим немного увеличивает hello аккумулятора, но оказывает влияние на hello монитор Engagement: продолжительность все сеансы и задания являются скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны). Мы рекомендуем использовать пороговое значение пакета не более 30 000 (30 с). Сохраненные журналы — это ограниченная too300 элементы. Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.

> [!WARNING]
> Порог повышения Hello не может быть tooa настроенный период меньше секунды. Если сделать это, hello SDK показывает трассировки с ошибкой hello и автоматически сбрасывает toohello значение по умолчанию, ноль секунд. Это hello tooreport триггеры SDK hello регистрирует в режиме реального времени.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
