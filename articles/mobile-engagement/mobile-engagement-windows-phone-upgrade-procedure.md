---
title: "aaaWindows процедуры обновления Phone Silverlight SDK"
description: "Процедуры обновления пакета SDK для Windows Phone Silverlight для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Процедуры обновления пакета SDK для Windows Phone Silverlight
Если уже имеется встроенный более старой версии нашего пакета SDK в приложение, у вас есть следующие точки, при обновлении hello SDK hello tooconsider.

Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello. Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.

## <a name="from-200-too330"></a>Из 2.0.0 too3.3.0
### <a name="test-logs"></a>Журналы тестирования
Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются. toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>Из 1.1.1 too2.0.0
Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения. Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов
> 
> 

При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.1.1 сначала затем применить после процедуры hello

### <a name="nuget-package"></a>Пакет NuGet
Замените **Capptain.WindowsPhone** на пакет NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Применение Служб мобильного взаимодействия
Hello SDK использует термин hello `Engagement`. Требуется tooupdate toomatch вашего проекта это изменение.

Необходимо toouninstall текущий пакет nuget Capptain. Советуем удалить все, что было изменено в папке ресурсов Capptain. Если требуется, чтобы tookeep эти файлы затем создается копия их.

После этого установите hello новый пакет nuget Microsoft Azure Engagement для вашего проекта. Его можно найти непосредственно на веб-сайте [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Это действие заменяет все файлы ресурсов используется охватом и добавляет новые Engagement DLL tooyour hello ссылки на проект.

У вас есть tooclean ссылки проекта, удалив ссылки на библиотеки DLL Capptain. Если этого не сделать, возникнет конфликт Capptain версии hello и будет происходить ошибки.

Если вы настроили Capptain ресурсы, скопируйте старые файлы содержимого и вставьте их в новых файлах Engagement hello. Обратите внимание, xaml и cs-файлы имеют toobe обновить.

После выполнения этих шагов вам достаточно tooreplace старые ссылки Capptain, новые ссылки Engagement hello.

1. Все пространства имен Capptain имеют toobe обновлены.
   
    Перед миграцией:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    После миграции:
   
        using Microsoft.Azure.Engagement;
2. Все классы Capptain, содержащие Capptain должны содержать Engagement.
   
    Перед миграцией:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    После миграции:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Для XAML-файлов изменятся также пространство имен и атрибуты Capptain.
   
    Перед миграцией:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    После миграции:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Для hello другие ресурсы, такие как рисунки Capptain Обратите внимание, что они также был переименован toouse «Занят».

### <a name="application-id--sdk-key"></a>Идентификатор приложения и ключ SDK
Engagement использует строку подключения. Не нужно toospecify идентификатора приложения и ключ SDK с мобильного охвата, имеется только toospecify строку подключения. Ее можно настроить в файле EngagementConfiguration.

Hello проектной конфигурации может быть задано в вашей `Resources\EngagementConfiguration.xml` файла проекта.

Измените этот файл toospecify:

* строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.

Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

Hello строку подключения для приложения отображается в hello классический портал Azure.

### <a name="items-name-change"></a>Изменение имени элементов
Каждый из элементов с именем *capptain* был переименован на *engagement*. Аналогичным образом, для *Capptain* слишком*Engagement*.

Примеры часто используемых элементов Capptain:

* CapptainConfiguration теперь называется EngagementConfiguration.
* CapptainAgent теперь называется EngagementAgent.
* CapptainReach теперь называется EngagementReach.
* CapptainHttpConfig теперь называется EngagementHttpConfig.
* GetCapptainPageName теперь называется GetEngagementPageName.

Обратите внимание, что переименование также влияет на переопределенные методы.

