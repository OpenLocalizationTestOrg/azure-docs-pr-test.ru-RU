---
title: "параметры для Azure Mobile Engagement Android SDK отчетов aaaAdvanced"
description: "Описывает, как toodo advanced analytics отчетов toocapture для Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Создание расширенных отчетов с помощью службы Engagement в Android
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

В этой статье описаны дополнительные сценарии создания отчетов в приложении Android. Можно применить эти параметры toohello приложения, созданные в hello [Приступая к работе](mobile-engagement-android-get-started.md) учебника.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

Учебник Hello все выполненные был намеренно прямой и простой, но такое расширенные параметры, которые можно выбрать.

## <a name="modifying-your-activity-classes"></a>Изменение классов `Activity`
В hello [учебник по началу работы](mobile-engagement-android-get-started.md), все бы toodo было toomake вашей `*Activity` подклассы наследуют от соответствующего hello `Engagement*Activity` классы. Например, если устаревшее действие расширяло `ListActivity`, нужно было обеспечить, чтобы оно расширяло и `EngagementListActivity`.

> [!IMPORTANT]
> При использовании `EngagementListActivity` или `EngagementExpandableListActivity`, убедитесь, что любой вызов слишком`requestWindowFeature(...);` выполняется до вызова hello слишком`super.onCreate(...);`, в противном случае происходит сбой.
> 
> 

Эти классы можно найти в hello `src` папке и скопируйте их в проект. классы Hello также находятся в hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную
Если невозможно или нежелательно toooverload вашей `Activity` классов, можно вместо этого начала и окончания действия пользователя путем вызова hello `EngagementAgent`его методы напрямую.

> [!IMPORTANT]
> Hello Android SDK никогда не вызывает hello `endActivity()` даже при закрытии приложения hello метод (в Android приложения никогда не закрыты). Таким образом, *высокой* рекомендуется toocall hello `startActivity()` метод в hello `onResume` обратного вызова *все* действия и hello `endActivity()` метод в hello `onPause()` обратный вызов из *все* ваши действия. Это hello единственным способом toobe убедиться, что сеансы не попадают. Если сеанс утечка, hello Engagement службы никогда не отключается от внутреннего сервера охвата hello, (поскольку служба hello остается подключенным, поскольку сеанс находится в состоянии ожидания).
> 
> 

Пример:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

Данный пример является аналогичные toohello `EngagementActivity` класс и его вариантов, исходный код которого приведен в hello `src` папки.

## <a name="using-applicationoncreate"></a>Использование Application.onCreate()
Любой код, поместите в `Application.onCreate()` и в другие приложения для вашего приложения процессов, включая службы Engagement hello выполняется обратных вызовов. Может иметь нежелательные побочные эффекты, как распределение памяти ненужные и потоков процесса hello обязательств или повторяющиеся широковещательных получателей или службы.

При переопределении `Application.onCreate()`, рекомендуется добавить следующий фрагмент кода в начале hello hello вашей `Application.onCreate()` функции:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Вам доступны такие же действия hello `Application.onTerminate()`, `Application.onLowMemory()`, и `Application.onConfigurationChanged(...)`.

Кроме того, можно расширить `EngagementApplication` вместо расширение `Application`: hello обратного вызова `Application.onCreate()` hello Проверка процесса и вызывает `Application.onApplicationProcessCreate()` только если hello текущий процесс не hello один hello Engagement службы размещения, hello и те же правила применяются для Здравствуйте других обратных вызовов.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Теги в файле AndroidManifest.xml hello
В теге hello службы в файле AndroidManifest.xml hello hello `android:label` атрибута можно toochoose имя hello hello службы Engagement отображенное tooend пользователей на экране «Запуск службы» Привет телефона. Рекомендуется, если для этого атрибута слишком`"<Your application name>Service"` (например, `"AcmeFunGameService"`).

Указание hello `android:process` атрибут обеспечивает hello, запускается служба участия в отдельном процессе (работающем участия в hello же процесс в приложение делает потенциально меньше реагировать main или UI-потока).

## <a name="building-with-proguard"></a>Создание приложения при помощи ProGuard
При создании пакета приложения с ProGuard tookeep необходимо некоторые классы. Можно использовать следующий фрагмент конфигурации hello.

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
