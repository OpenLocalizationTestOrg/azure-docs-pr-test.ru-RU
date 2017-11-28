---
title: "Пользователи tooindividual aaaPublish приложений в коллекцию Azure RemoteApp (Предварительная версия) | Документы Microsoft"
description: "Узнайте, как публиковать приложения tooindividual пользователей, а не в зависимости от группы в Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="6cf7c-103">Публикация приложений tooindividual пользователей в коллекции Azure RemoteApp (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="6cf7c-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6cf7c-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6cf7c-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6cf7c-106">В этой статье объясняется, как пользователи tooindividual toopublish приложений в коллекцию Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="6cf7c-107">Это новые функциональные возможности в Azure RemoteApp, в настоящее время в личной предварительной версии и первыми tooselect доступны только для ознакомительных целей.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="6cf7c-108">Первоначально Azure RemoteApp включен только один способ публикации приложений: Здравствуйте, администратор может опубликовать приложения из образа hello и могли бы быть видимым tooall пользователей в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="6cf7c-109">Распространенным сценарием является tooinclude многих приложений в одном образ и развертывать одной коллекции в порядке расходы на управление tooreduce.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="6cf7c-110">Зачастую не все приложения, соответствующие tooall пользователей — администраторы предпочли бы пользователей tooindividual toopublish приложения, они не увидят ненужные приложения, в приложении веб-канала.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="6cf7c-111">Теперь это возможно в Azure RemoteApp — в настоящее время в виде функции в ограниченной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="6cf7c-112">Вот краткое описание новых функциональных возможностей hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="6cf7c-113">Для коллекции можно настроить один из двух режимов.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="6cf7c-114">Hello исходный режим сбора, где все пользователи в коллекции могут просматривать все опубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="6cf7c-115">Это режим по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-115">This is hello default mode.</span></span>
   * <span data-ttu-id="6cf7c-116">новые приложения режим Hello, где пользователи видят только приложения, которые были явно назначены toothem</span><span class="sxs-lookup"><span data-stu-id="6cf7c-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="6cf7c-117">В момент hello режим приложения hello можно включить только с помощью командлетов Azure RemoteApp PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="6cf7c-118">Если установить tooapplication режим назначение пользователя в коллекции hello нельзя управлять с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="6cf7c-119">Назначение пользователя имеет toobe, управляемых с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="6cf7c-120">Пользователи будут видеть только приложения hello опубликованы непосредственно toothem.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="6cf7c-121">Однако по-прежнему возможно для других приложений, доступных на изображении hello Здравствуйте, toolaunch пользователя путем доступа к их непосредственно в операционной системе hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="6cf7c-122">Этот компонент не предоставляет безопасного блокировки приложений; ограничивает только видимости в приложение hello веб-канала.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="6cf7c-123">Если требуется, чтобы пользователи tooisolate из приложений, необходимо будет toouse отдельные коллекции для этого.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="6cf7c-124">Как tooget командлеты Azure RemoteApp PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cf7c-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="6cf7c-125">функциональность tootry hello новой предварительной версии, необходимо будет toouse командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6cf7c-126">Оно не возможные toouse hello Azure портала tooenable hello нового приложения публикации режим управления.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="6cf7c-127">Во-первых, убедитесь, что у вас есть hello [модуля Azure PowerShell](/powershell/azure/overview) установлен.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="6cf7c-128">Запустите консоль PowerShell hello в режиме администратора и выполнения hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="6cf7c-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="6cf7c-129">Он запросит имя пользователя и пароль Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="6cf7c-130">После входа командлеты Azure RemoteApp могут toorun будут выполняться для ваших подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="6cf7c-131">Как toocheck режим, который является коллекция в</span><span class="sxs-lookup"><span data-stu-id="6cf7c-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="6cf7c-132">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Проверьте режим сбора hello](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="6cf7c-134">Hello AclLevel свойство может иметь hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6cf7c-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="6cf7c-135">Сбор данных: hello исходной публикации режим.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="6cf7c-136">Все пользователи видят все опубликованные приложения.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-136">All users see all published apps.</span></span>
* <span data-ttu-id="6cf7c-137">Приложение: hello новой публикации режим.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="6cf7c-138">Пользователи видят только приложения hello непосредственно опубликованные toothem.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="6cf7c-139">Как режим публикации tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="6cf7c-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="6cf7c-140">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="6cf7c-141">Будут сохранены приложения состояния публикации: изначально все пользователи будут видеть все исходные опубликованные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="6cf7c-142">Как toolist пользователей, которые можно просмотреть определенное приложение</span><span class="sxs-lookup"><span data-stu-id="6cf7c-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="6cf7c-143">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="6cf7c-144">Это список всех пользователей, можно увидеть приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="6cf7c-145">Примечание: Вы увидите псевдонимы приложения hello (называемые «alias приложения» в синтаксисе hello выше), запустив Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="6cf7c-146">Как tooassign пользователь tooa приложения</span><span class="sxs-lookup"><span data-stu-id="6cf7c-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="6cf7c-147">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="6cf7c-148">Hello пользователь увидит приложения hello в клиенте Azure RemoteApp hello и может tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="6cf7c-149">Как tooremove приложения от пользователя</span><span class="sxs-lookup"><span data-stu-id="6cf7c-149">How tooremove an application from a user</span></span>
<span data-ttu-id="6cf7c-150">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="6cf7c-151">Обратная связь</span><span class="sxs-lookup"><span data-stu-id="6cf7c-151">Providing feedback</span></span>
<span data-ttu-id="6cf7c-152">Мы будем признательны за ваши отзывы и предложения относительно этой функции в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="6cf7c-153">Заполните hello [опроса](http://www.instant.ly/s/FDdrb) toolet нам о своих впечатлениях.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="6cf7c-154">Не было функцию предварительного просмотра hello вероятность tootry?</span><span class="sxs-lookup"><span data-stu-id="6cf7c-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="6cf7c-155">Если вы не участвовали в предварительной версии hello еще, используйте это [опроса](http://www.instant.ly/s/AY83p) toorequest доступа.</span><span class="sxs-lookup"><span data-stu-id="6cf7c-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

