---
title: "aaaUse командлеты PowerShell Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как toouse командлеты Windows PowerShell в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="adc27-103">Использование командлетов Windows PowerShell с Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="adc27-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="adc27-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="adc27-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="adc27-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="adc27-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="adc27-106">Можно использовать tooadminister командлеты Azure RemoteApp PowerShell hello и поддерживать вашей коллекции.</span><span class="sxs-lookup"><span data-stu-id="adc27-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="adc27-107">Используйте следующие сведения tooget работы hello.</span><span class="sxs-lookup"><span data-stu-id="adc27-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="adc27-108">Получить командлеты hello</span><span class="sxs-lookup"><span data-stu-id="adc27-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="adc27-109">Сначала загрузить командлеты Azure Powershell hello [здесь](http://go.microsoft.com/?linkid=9811175), командлетов RemoteApp hello включены в нем.</span><span class="sxs-lookup"><span data-stu-id="adc27-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="adc27-110">Извлечение hello [справки по командлетам Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="adc27-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="adc27-111">Настроить подписку toouse командлетов Azure</span><span class="sxs-lookup"><span data-stu-id="adc27-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="adc27-112">Выполните [в этом руководстве](/powershell/azure/overview) , можно использовать командлеты hello к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="adc27-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="adc27-113">Можно использовать эти действия tooget, быстро начать работу.</span><span class="sxs-lookup"><span data-stu-id="adc27-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="adc27-114">Загрузите и установите hello [командлетов Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="adc27-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="adc27-115">Запустите Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adc27-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="adc27-116">Запустите **Add-AzureAccount** tooauthenticate tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="adc27-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="adc27-117">При появлении запроса введите hello же имя пользователя и пароль, использовать toosign tooAzure портала.</span><span class="sxs-lookup"><span data-stu-id="adc27-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="adc27-118">Запустите **Get-AzureSubscription** toolist hello подписок, связанных с вашей учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="adc27-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="adc27-119">Запустите **Select-AzureSubscription - SubscriptionName &lt;имя подписки&gt;**  или **Select-AzureSubscription - SubscriptionId &lt;Код_подписки&gt;**  toouse подписки toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="adc27-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="adc27-120">Поздравляем, в консоли Azure PowerShell toouse настроен и готов.</span><span class="sxs-lookup"><span data-stu-id="adc27-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="adc27-121">Имейте в виду, что вам требуется toorepeate шаги 2 – 5 каждый раз при запуске консоли Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="adc27-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="adc27-122">Список всех коллекций</span><span class="sxs-lookup"><span data-stu-id="adc27-122">List all collections</span></span>
- - -
     <span data-ttu-id="adc27-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="adc27-124">Удаление коллекции</span><span class="sxs-lookup"><span data-stu-id="adc27-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="adc27-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="adc27-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="adc27-126">Пример: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="adc27-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="adc27-127">Создание облачной коллекции</span><span class="sxs-lookup"><span data-stu-id="adc27-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="adc27-128">Это просто, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="adc27-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="adc27-129">Hello выше команду автоматически публикует приложения Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio и Word).</span><span class="sxs-lookup"><span data-stu-id="adc27-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="adc27-130">Создание коллекции может занять 30 минут или дольше toocomplete.</span><span class="sxs-lookup"><span data-stu-id="adc27-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="adc27-131">В связи с этим команда возвращает идентификатор для отслеживания, который можно использовать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="adc27-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="adc27-132">После завершения hello коллекции можно добавить коллекцию toohello пользователей с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="adc27-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="adc27-133">Готово!</span><span class="sxs-lookup"><span data-stu-id="adc27-133">And you're done!</span></span> <span data-ttu-id="adc27-134">Этот пользователь должен быть может tooconnect toohello приложения с помощью клиента Azure RemoteApp hello найден [здесь](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="adc27-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="adc27-135">Доступные командлеты</span><span class="sxs-lookup"><span data-stu-id="adc27-135">Available cmdlets</span></span>
<span data-ttu-id="adc27-136">Существует множество других команд, которые у нас есть, вскоре будет реализована hello документации для них:</span><span class="sxs-lookup"><span data-stu-id="adc27-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="adc27-137">Основные командлеты для коллекций RemoteApp</span><span class="sxs-lookup"><span data-stu-id="adc27-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="adc27-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="adc27-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="adc27-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="adc27-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="adc27-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="adc27-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="adc27-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="adc27-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="adc27-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="adc27-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="adc27-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="adc27-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="adc27-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="adc27-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="adc27-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="adc27-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="adc27-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="adc27-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="adc27-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="adc27-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="adc27-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="adc27-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="adc27-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="adc27-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="adc27-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="adc27-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="adc27-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="adc27-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="adc27-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="adc27-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="adc27-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="adc27-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="adc27-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="adc27-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="adc27-157">Командлеты для виртуальных сетей RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="adc27-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="adc27-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="adc27-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="adc27-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="adc27-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="adc27-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="adc27-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="adc27-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="adc27-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="adc27-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="adc27-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="adc27-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="adc27-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="adc27-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="adc27-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="adc27-165">Командлеты для шаблонов образов RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="adc27-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="adc27-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="adc27-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="adc27-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="adc27-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="adc27-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="adc27-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="adc27-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="adc27-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="adc27-170">Другие командлеты RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="adc27-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="adc27-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="adc27-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="adc27-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="adc27-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="adc27-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="adc27-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="adc27-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="adc27-174">Get-AzureRemoteAppOperationResult</span></span>

