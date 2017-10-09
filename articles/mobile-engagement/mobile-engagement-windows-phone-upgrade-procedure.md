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
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="d813a-103">Процедуры обновления пакета SDK для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d813a-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="d813a-104">Если уже имеется встроенный более старой версии нашего пакета SDK в приложение, у вас есть следующие точки, при обновлении hello SDK hello tooconsider.</span><span class="sxs-lookup"><span data-stu-id="d813a-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="d813a-105">Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="d813a-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="d813a-106">Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.</span><span class="sxs-lookup"><span data-stu-id="d813a-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="d813a-107">Из 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="d813a-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="d813a-108">Журналы тестирования</span><span class="sxs-lookup"><span data-stu-id="d813a-108">Test logs</span></span>
<span data-ttu-id="d813a-109">Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются.</span><span class="sxs-lookup"><span data-stu-id="d813a-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="d813a-110">toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:</span><span class="sxs-lookup"><span data-stu-id="d813a-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="d813a-111">Из 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="d813a-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="d813a-112">Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d813a-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d813a-113">Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="d813a-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="d813a-114">Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов</span><span class="sxs-lookup"><span data-stu-id="d813a-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="d813a-115">При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.1.1 сначала затем применить после процедуры hello</span><span class="sxs-lookup"><span data-stu-id="d813a-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="d813a-116">Пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="d813a-116">Nuget package</span></span>
<span data-ttu-id="d813a-117">Замените **Capptain.WindowsPhone** на пакет NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="d813a-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="d813a-118">Применение Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="d813a-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="d813a-119">Hello SDK использует термин hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="d813a-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="d813a-120">Требуется tooupdate toomatch вашего проекта это изменение.</span><span class="sxs-lookup"><span data-stu-id="d813a-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="d813a-121">Необходимо toouninstall текущий пакет nuget Capptain.</span><span class="sxs-lookup"><span data-stu-id="d813a-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="d813a-122">Советуем удалить все, что было изменено в папке ресурсов Capptain.</span><span class="sxs-lookup"><span data-stu-id="d813a-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="d813a-123">Если требуется, чтобы tookeep эти файлы затем создается копия их.</span><span class="sxs-lookup"><span data-stu-id="d813a-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="d813a-124">После этого установите hello новый пакет nuget Microsoft Azure Engagement для вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="d813a-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="d813a-125">Его можно найти непосредственно на веб-сайте [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="d813a-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="d813a-126">Это действие заменяет все файлы ресурсов используется охватом и добавляет новые Engagement DLL tooyour hello ссылки на проект.</span><span class="sxs-lookup"><span data-stu-id="d813a-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="d813a-127">У вас есть tooclean ссылки проекта, удалив ссылки на библиотеки DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="d813a-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="d813a-128">Если этого не сделать, возникнет конфликт Capptain версии hello и будет происходить ошибки.</span><span class="sxs-lookup"><span data-stu-id="d813a-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="d813a-129">Если вы настроили Capptain ресурсы, скопируйте старые файлы содержимого и вставьте их в новых файлах Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="d813a-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="d813a-130">Обратите внимание, xaml и cs-файлы имеют toobe обновить.</span><span class="sxs-lookup"><span data-stu-id="d813a-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="d813a-131">После выполнения этих шагов вам достаточно tooreplace старые ссылки Capptain, новые ссылки Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="d813a-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="d813a-132">Все пространства имен Capptain имеют toobe обновлены.</span><span class="sxs-lookup"><span data-stu-id="d813a-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="d813a-133">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="d813a-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="d813a-134">После миграции:</span><span class="sxs-lookup"><span data-stu-id="d813a-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="d813a-135">Все классы Capptain, содержащие Capptain должны содержать Engagement.</span><span class="sxs-lookup"><span data-stu-id="d813a-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="d813a-136">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="d813a-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="d813a-137">После миграции:</span><span class="sxs-lookup"><span data-stu-id="d813a-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="d813a-138">Для XAML-файлов изменятся также пространство имен и атрибуты Capptain.</span><span class="sxs-lookup"><span data-stu-id="d813a-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="d813a-139">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="d813a-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="d813a-140">После миграции:</span><span class="sxs-lookup"><span data-stu-id="d813a-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="d813a-141">Для hello другие ресурсы, такие как рисунки Capptain Обратите внимание, что они также был переименован toouse «Занят».</span><span class="sxs-lookup"><span data-stu-id="d813a-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="d813a-142">Идентификатор приложения и ключ SDK</span><span class="sxs-lookup"><span data-stu-id="d813a-142">Application ID / SDK Key</span></span>
<span data-ttu-id="d813a-143">Engagement использует строку подключения.</span><span class="sxs-lookup"><span data-stu-id="d813a-143">Engagement uses a connection string.</span></span> <span data-ttu-id="d813a-144">Не нужно toospecify идентификатора приложения и ключ SDK с мобильного охвата, имеется только toospecify строку подключения.</span><span class="sxs-lookup"><span data-stu-id="d813a-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="d813a-145">Ее можно настроить в файле EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d813a-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="d813a-146">Hello проектной конфигурации может быть задано в вашей `Resources\EngagementConfiguration.xml` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="d813a-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="d813a-147">Измените этот файл toospecify:</span><span class="sxs-lookup"><span data-stu-id="d813a-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="d813a-148">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="d813a-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="d813a-149">Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="d813a-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="d813a-150">Hello строку подключения для приложения отображается в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d813a-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="d813a-151">Изменение имени элементов</span><span class="sxs-lookup"><span data-stu-id="d813a-151">Items name change</span></span>
<span data-ttu-id="d813a-152">Каждый из элементов с именем *capptain* был переименован на *engagement*.</span><span class="sxs-lookup"><span data-stu-id="d813a-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="d813a-153">Аналогичным образом, для *Capptain* слишком*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="d813a-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="d813a-154">Примеры часто используемых элементов Capptain:</span><span class="sxs-lookup"><span data-stu-id="d813a-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="d813a-155">CapptainConfiguration теперь называется EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d813a-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="d813a-156">CapptainAgent теперь называется EngagementAgent.</span><span class="sxs-lookup"><span data-stu-id="d813a-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="d813a-157">CapptainReach теперь называется EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="d813a-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="d813a-158">CapptainHttpConfig теперь называется EngagementHttpConfig.</span><span class="sxs-lookup"><span data-stu-id="d813a-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="d813a-159">GetCapptainPageName теперь называется GetEngagementPageName.</span><span class="sxs-lookup"><span data-stu-id="d813a-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="d813a-160">Обратите внимание, что переименование также влияет на переопределенные методы.</span><span class="sxs-lookup"><span data-stu-id="d813a-160">Note that rename also affects overridden methods.</span></span>

