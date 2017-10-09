---
title: "aaaEnable подключение к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell"
description: "Как tooconfigure azure облачные приложения службы с помощью подключения удаленного рабочего стола tooallow PowerShell"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="62ff8-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="62ff8-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62ff8-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="62ff8-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="62ff8-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="62ff8-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="62ff8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62ff8-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="62ff8-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62ff8-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="62ff8-108">Удаленный рабочий стол позволяет tooaccess hello системной роли, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="62ff8-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="62ff8-109">Можно использовать tootroubleshoot подключения удаленного рабочего стола и диагностировать проблемы с приложением во время его выполнения.</span><span class="sxs-lookup"><span data-stu-id="62ff8-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="62ff8-110">В этой статье описывается как tooenable удаленного рабочего стола на роли облачной службы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62ff8-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="62ff8-111">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи.</span><span class="sxs-lookup"><span data-stu-id="62ff8-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="62ff8-112">PowerShell использует hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, после развертывания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="62ff8-113">Настройка удаленного рабочего стола с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="62ff8-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="62ff8-114">Hello [AzureServiceRemoteDesktopExtension набор](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлет позволяет tooenable удаленного рабочего стола на указанные роли или все роли из развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="62ff8-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="62ff8-115">Hello командлета вы можете задать hello имя пользователя и пароль для hello пользователя удаленного рабочего стола через hello *учетные данные* параметр, который принимает объект PSCredential.</span><span class="sxs-lookup"><span data-stu-id="62ff8-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="62ff8-116">Если вы используете PowerShell интерактивно, можно легко задавать hello объекта PSCredential, вызывающему Привет [учетные данные Get](https://technet.microsoft.com/library/hh849815.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="62ff8-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="62ff8-117">Эта команда отображает диалоговое окно, позволяя вам tooenter hello имя пользователя и пароль для удаленного пользователя hello в безопасном режиме.</span><span class="sxs-lookup"><span data-stu-id="62ff8-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="62ff8-118">Так как в сценариях автоматизации помогает PowerShell, можно также настроить hello **PSCredential** объекта таким образом, не требующее вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="62ff8-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="62ff8-119">Во-первых необходимо tooset безопасный пароль.</span><span class="sxs-lookup"><span data-stu-id="62ff8-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="62ff8-120">Начать с указанием незашифрованный пароль преобразовать tooa защищенной строки с помощью [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ff8-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="62ff8-121">Затем следует записать tooconvert этой защищенной строки в зашифрованную стандартную строку с помощью [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ff8-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="62ff8-122">Теперь можно сохранить этот файл tooa зашифрованную стандартную строку с помощью [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ff8-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="62ff8-123">Также можно создать файл надежный пароль, поэтому, не tootype в hello пароль каждый раз.</span><span class="sxs-lookup"><span data-stu-id="62ff8-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="62ff8-124">Кроме того, файл с надежным паролем безопаснее, чем обычный текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="62ff8-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="62ff8-125">Используйте следующие toocreate PowerShell файл безопасного пароля hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="62ff8-126">При задании пароля hello, убедитесь, что выполнены hello [требованиям сложности](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ff8-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="62ff8-127">toocreate hello объекта учетных данных из файла hello надежный пароль, необходимо прочитать содержимое файла hello и преобразовать их назад tooa secure строки с помощью [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ff8-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="62ff8-128">Hello [набор AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлет также принимает *истечение срока действия* параметр, который задает **DateTime** пользовательских hello срок действия учетной записи.</span><span class="sxs-lookup"><span data-stu-id="62ff8-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="62ff8-129">Например можно задать tooexpire hello учетную запись на несколько дней из hello текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="62ff8-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="62ff8-130">В этом примере PowerShell показано, как tooset hello расширения удаленного рабочего стола в облачной службе:</span><span class="sxs-lookup"><span data-stu-id="62ff8-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="62ff8-131">Также при необходимости можно указать слот развертывания hello и роли, которые вы хотите tooenable удаленного рабочего стола на.</span><span class="sxs-lookup"><span data-stu-id="62ff8-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="62ff8-132">Если эти параметры не указаны, hello включает удаленный рабочий стол для всех ролей в hello **рабочей** слот развертывания.</span><span class="sxs-lookup"><span data-stu-id="62ff8-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="62ff8-133">Hello расширения удаленного рабочего стола связанной с развертыванием.</span><span class="sxs-lookup"><span data-stu-id="62ff8-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="62ff8-134">Если вы создаете новое развертывание для службы hello, у вас есть удаленного рабочего стола tooenable развертывания.</span><span class="sxs-lookup"><span data-stu-id="62ff8-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="62ff8-135">Если требуется всегда toohave включен удаленный рабочий стол, следует рассмотреть, интеграция hello сценариев PowerShell в рабочий процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="62ff8-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="62ff8-136">Подключение к экземпляру роли по протоколу удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="62ff8-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="62ff8-137">Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) командлета — используется tooremote рабочего стола к определенного экземпляра роли облачной службы.</span><span class="sxs-lookup"><span data-stu-id="62ff8-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="62ff8-138">Можно использовать hello *LocalPath* файл hello toodownload параметр протокола удаленного рабочего СТОЛА на компьютере.</span><span class="sxs-lookup"><span data-stu-id="62ff8-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="62ff8-139">Или можно использовать hello *запуска* диалоговое окно параметров toodirectly запуска hello удаленный рабочий стол tooaccess hello экземпляра роли облачной службы.</span><span class="sxs-lookup"><span data-stu-id="62ff8-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="62ff8-140">Убедитесь, что расширение удаленного рабочего стола включено в службе.</span><span class="sxs-lookup"><span data-stu-id="62ff8-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="62ff8-141">Hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) показывает, включен или отключен на развертывание службы удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="62ff8-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="62ff8-142">Hello командлет возвращает hello имя пользователя для пользователя удаленного рабочего стола hello и hello роли, которые hello удаленного рабочего стола расширение включено для.</span><span class="sxs-lookup"><span data-stu-id="62ff8-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="62ff8-143">По умолчанию это происходит на слот развертывания hello и toouse hello промежуточных слотах, вместо этого можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="62ff8-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="62ff8-144">Удаление расширения удаленного рабочего стола из службы</span><span class="sxs-lookup"><span data-stu-id="62ff8-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="62ff8-145">При включении удаленного рабочего стола расширения hello в развертывании, и требуется tooupdate hello настройки удаленного рабочего стола, сначала удалите расширение hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="62ff8-146">И снова включите его с новыми настройками hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="62ff8-147">Например если требуется, чтобы tooset новый пароль для учетной записи удаленного пользователя hello или hello срок действия истек.</span><span class="sxs-lookup"><span data-stu-id="62ff8-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="62ff8-148">Это требуется в существующих развертываниях расширением hello удаленного рабочего стола включена.</span><span class="sxs-lookup"><span data-stu-id="62ff8-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="62ff8-149">Для новых развертываний можно просто применить расширения hello напрямую.</span><span class="sxs-lookup"><span data-stu-id="62ff8-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="62ff8-150">tooremove hello удаленного рабочего стола расширения из hello развертывания, можно использовать hello [AzureServiceRemoteDesktopExtension удаление](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="62ff8-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="62ff8-151">Также при необходимости можно указать слот развертывания hello и роли, из которого нужно tooremove hello удаленного рабочего стола расширения.</span><span class="sxs-lookup"><span data-stu-id="62ff8-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="62ff8-152">hello расширения toocompletely удалить конфигурацию необходимо вызвать hello *удалить* командлет с hello **UninstallConfiguration** параметра.</span><span class="sxs-lookup"><span data-stu-id="62ff8-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="62ff8-153">Hello **UninstallConfiguration** параметр удаляет все конфигурации расширения, примененные toohello службы.</span><span class="sxs-lookup"><span data-stu-id="62ff8-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="62ff8-154">Все конфигурации расширения связан с конфигурацией службы hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="62ff8-155">Вызов hello *удалить* командлета без **UninstallConfiguration** отсоединяет hello <mark>развертывания</mark> из конфигурации расширения hello, поэтому фактически удаляется расширение Hello.</span><span class="sxs-lookup"><span data-stu-id="62ff8-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="62ff8-156">Тем не менее Настройка расширения hello остается связанным с hello службы.</span><span class="sxs-lookup"><span data-stu-id="62ff8-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="62ff8-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="62ff8-157">Additional resources</span></span>

<span data-ttu-id="62ff8-158">[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="62ff8-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
