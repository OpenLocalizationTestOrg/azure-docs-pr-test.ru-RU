---
title: "Дополнительные возможности создания отчетов пакета SDK для Android в Службах мобильного взаимодействия Azure"
description: "Описание создания расширенных отчетов для записи данных аналитики для пакета SDK для Android в Службах мобильного взаимодействия Azure."
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
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="ea963-103">Создание расширенных отчетов с помощью службы Engagement в Android</span><span class="sxs-lookup"><span data-stu-id="ea963-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea963-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="ea963-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="ea963-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ea963-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ea963-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ea963-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ea963-107">Android</span><span class="sxs-lookup"><span data-stu-id="ea963-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="ea963-108">В этой статье описаны дополнительные сценарии создания отчетов в приложении Android.</span><span class="sxs-lookup"><span data-stu-id="ea963-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="ea963-109">Эти параметры можно применить для приложения, созданного в учебнике [по началу работы](mobile-engagement-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="ea963-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea963-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea963-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="ea963-111">Для изученного учебника были намеренно подобраны понятные и простые задания, однако для выбора доступны и дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="ea963-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="ea963-112">Изменение классов `Activity`</span><span class="sxs-lookup"><span data-stu-id="ea963-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="ea963-113">В [руководстве по началу работы](mobile-engagement-android-get-started.md) достаточно было обеспечить наследование подклассов `*Activity` из соответствующих классов `Engagement*Activity`.</span><span class="sxs-lookup"><span data-stu-id="ea963-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="ea963-114">Например, если устаревшее действие расширяло `ListActivity`, нужно было обеспечить, чтобы оно расширяло и `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="ea963-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea963-115">При использовании `EngagementListActivity` или `EngagementExpandableListActivity` необходимо обеспечить, чтобы любой вызов `requestWindowFeature(...);` выполнялся до вызова `super.onCreate(...);`, в противном случае произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="ea963-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="ea963-116">Эти классы можно найти в папке `src` и скопировать их в проект.</span><span class="sxs-lookup"><span data-stu-id="ea963-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="ea963-117">Данные классы также представлены в **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="ea963-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="ea963-118">Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="ea963-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="ea963-119">Если вы не можете перегружать классы `Activity` или не хотите этого делать, можно запускать и завершать действия, вызывая методы `EngagementAgent` напрямую.</span><span class="sxs-lookup"><span data-stu-id="ea963-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea963-120">Пакет SDK для Android никогда не вызывает метод `endActivity()`, даже если приложение закрыто (на Android приложения никогда не закрываются).</span><span class="sxs-lookup"><span data-stu-id="ea963-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="ea963-121">Поэтому *настоятельно* рекомендуется вызывать метод `startActivity()` в обратном вызове `onResume` *всех* действий, а метод `endActivity()` в обратном вызове `onPause()` *всех* действий.</span><span class="sxs-lookup"><span data-stu-id="ea963-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="ea963-122">Это единственный способ гарантировать отсутствие утечки сеансов.</span><span class="sxs-lookup"><span data-stu-id="ea963-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="ea963-123">Если наблюдается утечка сеанса, служба Engagement никогда не отключится от внутреннего сервера Engagement (так как служба остается подключенной до тех пор, пока сеанс находится в состоянии ожидания).</span><span class="sxs-lookup"><span data-stu-id="ea963-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="ea963-124">Пример:</span><span class="sxs-lookup"><span data-stu-id="ea963-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="ea963-125">Этот пример похож на класс `EngagementActivity` и его варианты, исходный код которых предоставляется в папке `src`.</span><span class="sxs-lookup"><span data-stu-id="ea963-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="ea963-126">Использование Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="ea963-126">Using Application.onCreate()</span></span>
<span data-ttu-id="ea963-127">Любой код, помещаемый в `Application.onCreate()` и другие обратные вызовы приложения, выполняется для всех процессов приложения, включая службу Engagement.</span><span class="sxs-lookup"><span data-stu-id="ea963-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="ea963-128">При этом возможны нежелательные побочные эффекты, например выделение ненужной памяти и потоки в процессе Engagement, повторяющиеся получатели рассылки или службы.</span><span class="sxs-lookup"><span data-stu-id="ea963-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="ea963-129">При переопределении `Application.onCreate()` рекомендуется добавить следующий фрагмент кода в начало функции `Application.onCreate()`.</span><span class="sxs-lookup"><span data-stu-id="ea963-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="ea963-130">То же самое можно сделать для `Application.onTerminate()`, `Application.onLowMemory()` и `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="ea963-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="ea963-131">Вы можете также расширить `EngagementApplication` вместо расширения `Application`: обратный вызов `Application.onCreate()` проверяет процесс и вызывает `Application.onApplicationProcessCreate()` только в том случае, если текущий процесс не размещает службу Engagement. Эти же правила применяются к другим обратным вызовам.</span><span class="sxs-lookup"><span data-stu-id="ea963-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="ea963-132">Теги в файле AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="ea963-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="ea963-133">Атрибут `android:label` тега службы в файле AndroidManifest.xml позволяет выбрать имя службы Engagement в том виде, в каком оно выводится для конечных пользователей на экране "Running Services" (Работающие службы) их телефонов.</span><span class="sxs-lookup"><span data-stu-id="ea963-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="ea963-134">Рекомендуется задать для этого атрибута значение `"<Your application name>Service"` (например, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="ea963-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="ea963-135">Задание атрибута `android:process` гарантирует, что служба Engagement будет запускаться в своем собственном процессе (запуск службы Engagement в одном процессе с приложением может привести к тому, что основной поток (поток пользовательского интерфейса) станет хуже реагировать).</span><span class="sxs-lookup"><span data-stu-id="ea963-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="ea963-136">Создание приложения при помощи ProGuard</span><span class="sxs-lookup"><span data-stu-id="ea963-136">Building with ProGuard</span></span>
<span data-ttu-id="ea963-137">При создании пакета приложения с помощью ProGuard необходимо сохранить некоторые классы.</span><span class="sxs-lookup"><span data-stu-id="ea963-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="ea963-138">Можно использовать следующие фрагменты кода конфигурации:</span><span class="sxs-lookup"><span data-stu-id="ea963-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
