---
title: "Использование командлетов PowerShell с Azure RemoteApp | Документация Майкрософт"
description: "Узнайте, как использовать командлеты Windows PowerShell в Azure RemoteApp."
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
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="d2b8c-103">Использование командлетов Windows PowerShell с Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d2b8c-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d2b8c-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d2b8c-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="d2b8c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="d2b8c-106">Для администрирования и обслуживания коллекций можно использовать командлеты PowerShell для Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="d2b8c-107">Используйте следующие сведения, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="d2b8c-108">Загрузка командлетов</span><span class="sxs-lookup"><span data-stu-id="d2b8c-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="d2b8c-109">Сначала скачайте командлеты Azure PowerShell [отсюда](http://go.microsoft.com/?linkid=9811175). В их состав уже входят командлеты RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="d2b8c-110">Изучите [справку по командлетам Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="d2b8c-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="d2b8c-111">Настройка командлетов Azure для работы с подпиской</span><span class="sxs-lookup"><span data-stu-id="d2b8c-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="d2b8c-112">С помощью [этого руководства](/powershell/azure/overview) вы сможете сделать так, чтобы командлеты можно было использовать с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="d2b8c-113">Чтобы быстро приступить к работе:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="d2b8c-114">Скачайте и установите [командлеты Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="d2b8c-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="d2b8c-115">Запустите Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="d2b8c-116">Выполните команду **Add-AzureAccount** для аутентификации в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="d2b8c-117">При появлении запроса введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="d2b8c-118">Выполните команду **Get-AzureSubscription** , чтобы получить список подписок, связанных с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="d2b8c-119">Выполните команду **Select-AzureSubscription -SubscriptionName &lt;название подписки&gt;** или **Select-AzureSubscription -SubscriptionId &lt;ИД подписки&gt;**, чтобы указать подписку, которую следует использовать.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="d2b8c-120">Поздравляем, консоль Azure PowerShell настроена и готова к работе.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="d2b8c-121">Имейте в виду, что вам потребуется повторять шаги 2–5 при каждом запуске консоли Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="d2b8c-122">Список всех коллекций</span><span class="sxs-lookup"><span data-stu-id="d2b8c-122">List all collections</span></span>
- - -
     <span data-ttu-id="d2b8c-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="d2b8c-124">Удаление коллекции</span><span class="sxs-lookup"><span data-stu-id="d2b8c-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="d2b8c-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="d2b8c-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="d2b8c-126">Пример: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="d2b8c-127">Создание облачной коллекции</span><span class="sxs-lookup"><span data-stu-id="d2b8c-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="d2b8c-128">Это просто. Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="d2b8c-129">Приведенная выше команда автоматически публикует приложения Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio и Word).</span><span class="sxs-lookup"><span data-stu-id="d2b8c-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="d2b8c-130">Для создания коллекции может потребоваться 30 или более минут.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="d2b8c-131">В связи с этим команда возвращает идентификатор для отслеживания, который можно использовать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="d2b8c-132">После создания коллекции в нее можно добавить пользователей с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="d2b8c-133">Готово!</span><span class="sxs-lookup"><span data-stu-id="d2b8c-133">And you're done!</span></span> <span data-ttu-id="d2b8c-134">Этот пользователь сможет подключиться к приложению с помощью клиента Azure RemoteApp, который можно найти [здесь](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2b8c-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="d2b8c-135">Доступные командлеты</span><span class="sxs-lookup"><span data-stu-id="d2b8c-135">Available cmdlets</span></span>
<span data-ttu-id="d2b8c-136">Доступно множество других команд, документация для которых скоро будет опубликована.</span><span class="sxs-lookup"><span data-stu-id="d2b8c-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="d2b8c-137">Основные командлеты для коллекций RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d2b8c-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="d2b8c-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="d2b8c-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="d2b8c-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="d2b8c-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="d2b8c-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="d2b8c-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="d2b8c-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="d2b8c-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="d2b8c-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="d2b8c-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="d2b8c-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="d2b8c-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="d2b8c-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="d2b8c-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="d2b8c-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="d2b8c-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="d2b8c-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="d2b8c-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="d2b8c-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="d2b8c-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="d2b8c-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="d2b8c-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="d2b8c-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="d2b8c-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="d2b8c-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="d2b8c-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="d2b8c-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="d2b8c-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="d2b8c-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="d2b8c-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="d2b8c-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="d2b8c-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="d2b8c-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="d2b8c-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="d2b8c-157">Командлеты для виртуальных сетей RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="d2b8c-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="d2b8c-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="d2b8c-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="d2b8c-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="d2b8c-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="d2b8c-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="d2b8c-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="d2b8c-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="d2b8c-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="d2b8c-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="d2b8c-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="d2b8c-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="d2b8c-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="d2b8c-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="d2b8c-165">Командлеты для шаблонов образов RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="d2b8c-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="d2b8c-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="d2b8c-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="d2b8c-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="d2b8c-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="d2b8c-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="d2b8c-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="d2b8c-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="d2b8c-170">Другие командлеты RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="d2b8c-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="d2b8c-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="d2b8c-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="d2b8c-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="d2b8c-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="d2b8c-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="d2b8c-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="d2b8c-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="d2b8c-174">Get-AzureRemoteAppOperationResult</span></span>

