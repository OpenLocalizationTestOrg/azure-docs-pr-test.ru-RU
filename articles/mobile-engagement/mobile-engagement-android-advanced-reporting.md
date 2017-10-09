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
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="843de-103">Создание расширенных отчетов с помощью службы Engagement в Android</span><span class="sxs-lookup"><span data-stu-id="843de-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="843de-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="843de-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="843de-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="843de-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="843de-106">iOS</span><span class="sxs-lookup"><span data-stu-id="843de-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="843de-107">Android</span><span class="sxs-lookup"><span data-stu-id="843de-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="843de-108">В этой статье описаны дополнительные сценарии создания отчетов в приложении Android.</span><span class="sxs-lookup"><span data-stu-id="843de-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="843de-109">Можно применить эти параметры toohello приложения, созданные в hello [Приступая к работе](mobile-engagement-android-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="843de-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="843de-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="843de-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="843de-111">Учебник Hello все выполненные был намеренно прямой и простой, но такое расширенные параметры, которые можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="843de-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="843de-112">Изменение классов `Activity`</span><span class="sxs-lookup"><span data-stu-id="843de-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="843de-113">В hello [учебник по началу работы](mobile-engagement-android-get-started.md), все бы toodo было toomake вашей `*Activity` подклассы наследуют от соответствующего hello `Engagement*Activity` классы.</span><span class="sxs-lookup"><span data-stu-id="843de-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="843de-114">Например, если устаревшее действие расширяло `ListActivity`, нужно было обеспечить, чтобы оно расширяло и `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="843de-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="843de-115">При использовании `EngagementListActivity` или `EngagementExpandableListActivity`, убедитесь, что любой вызов слишком`requestWindowFeature(...);` выполняется до вызова hello слишком`super.onCreate(...);`, в противном случае происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="843de-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="843de-116">Эти классы можно найти в hello `src` папке и скопируйте их в проект.</span><span class="sxs-lookup"><span data-stu-id="843de-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="843de-117">классы Hello также находятся в hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="843de-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="843de-118">Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="843de-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="843de-119">Если невозможно или нежелательно toooverload вашей `Activity` классов, можно вместо этого начала и окончания действия пользователя путем вызова hello `EngagementAgent`его методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="843de-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="843de-120">Hello Android SDK никогда не вызывает hello `endActivity()` даже при закрытии приложения hello метод (в Android приложения никогда не закрыты).</span><span class="sxs-lookup"><span data-stu-id="843de-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="843de-121">Таким образом, *высокой* рекомендуется toocall hello `startActivity()` метод в hello `onResume` обратного вызова *все* действия и hello `endActivity()` метод в hello `onPause()` обратный вызов из *все* ваши действия.</span><span class="sxs-lookup"><span data-stu-id="843de-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="843de-122">Это hello единственным способом toobe убедиться, что сеансы не попадают.</span><span class="sxs-lookup"><span data-stu-id="843de-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="843de-123">Если сеанс утечка, hello Engagement службы никогда не отключается от внутреннего сервера охвата hello, (поскольку служба hello остается подключенным, поскольку сеанс находится в состоянии ожидания).</span><span class="sxs-lookup"><span data-stu-id="843de-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="843de-124">Пример:</span><span class="sxs-lookup"><span data-stu-id="843de-124">Here is an example:</span></span>

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

<span data-ttu-id="843de-125">Данный пример является аналогичные toohello `EngagementActivity` класс и его вариантов, исходный код которого приведен в hello `src` папки.</span><span class="sxs-lookup"><span data-stu-id="843de-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="843de-126">Использование Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="843de-126">Using Application.onCreate()</span></span>
<span data-ttu-id="843de-127">Любой код, поместите в `Application.onCreate()` и в другие приложения для вашего приложения процессов, включая службы Engagement hello выполняется обратных вызовов.</span><span class="sxs-lookup"><span data-stu-id="843de-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="843de-128">Может иметь нежелательные побочные эффекты, как распределение памяти ненужные и потоков процесса hello обязательств или повторяющиеся широковещательных получателей или службы.</span><span class="sxs-lookup"><span data-stu-id="843de-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="843de-129">При переопределении `Application.onCreate()`, рекомендуется добавить следующий фрагмент кода в начале hello hello вашей `Application.onCreate()` функции:</span><span class="sxs-lookup"><span data-stu-id="843de-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="843de-130">Вам доступны такие же действия hello `Application.onTerminate()`, `Application.onLowMemory()`, и `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="843de-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="843de-131">Кроме того, можно расширить `EngagementApplication` вместо расширение `Application`: hello обратного вызова `Application.onCreate()` hello Проверка процесса и вызывает `Application.onApplicationProcessCreate()` только если hello текущий процесс не hello один hello Engagement службы размещения, hello и те же правила применяются для Здравствуйте других обратных вызовов.</span><span class="sxs-lookup"><span data-stu-id="843de-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="843de-132">Теги в файле AndroidManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="843de-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="843de-133">В теге hello службы в файле AndroidManifest.xml hello hello `android:label` атрибута можно toochoose имя hello hello службы Engagement отображенное tooend пользователей на экране «Запуск службы» Привет телефона.</span><span class="sxs-lookup"><span data-stu-id="843de-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="843de-134">Рекомендуется, если для этого атрибута слишком`"<Your application name>Service"` (например, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="843de-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="843de-135">Указание hello `android:process` атрибут обеспечивает hello, запускается служба участия в отдельном процессе (работающем участия в hello же процесс в приложение делает потенциально меньше реагировать main или UI-потока).</span><span class="sxs-lookup"><span data-stu-id="843de-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="843de-136">Создание приложения при помощи ProGuard</span><span class="sxs-lookup"><span data-stu-id="843de-136">Building with ProGuard</span></span>
<span data-ttu-id="843de-137">При создании пакета приложения с ProGuard tookeep необходимо некоторые классы.</span><span class="sxs-lookup"><span data-stu-id="843de-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="843de-138">Можно использовать следующий фрагмент конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="843de-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
