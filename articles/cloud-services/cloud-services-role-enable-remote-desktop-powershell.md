---
title: "Включение подключения к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell"
description: "Как настроить приложение облачной службы Azure для подключений к удаленному рабочему столу с помощью PowerShell"
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
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="e9c0f-103">Включение подключения к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9c0f-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9c0f-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="e9c0f-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="e9c0f-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e9c0f-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="e9c0f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9c0f-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="e9c0f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9c0f-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="e9c0f-108">С помощью удаленного рабочего стола обеспечивается доступ к рабочему столу экземпляра, работающего в Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="e9c0f-109">Подключение к удаленному рабочему столу позволяет диагностировать и устранять неполадки выполняющегося приложения.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="e9c0f-110">В этой статье описывается включение удаленного рабочего стола для ролей облачной службы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="e9c0f-111">Сведения о компонентах, которые потребуются для выполнения инструкций в этой статье, см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="e9c0f-112">В PowerShell используется расширение удаленного рабочего стола, поэтому удаленный рабочий стол можно включить даже после развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="e9c0f-113">Настройка удаленного рабочего стола с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9c0f-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="e9c0f-114">Командлет [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) позволяет включить удаленный рабочий стол для всех или некоторых ролей в развернутой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="e9c0f-115">Он позволяет указать имя и пароль пользователя удаленного рабочего стола с помощью параметра *Credential* , который принимает объект PSCredential.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="e9c0f-116">Если вы используете PowerShell в интерактивном режиме, то можете задать объект PSCredential, вызвав командлет [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e9c0f-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="e9c0f-117">Эта команда открывает диалоговое окно, в котором вы сможете в защищенном режиме указать имя и пароль удаленного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="e9c0f-118">Так как PowerShell используется в сценариях автоматизации, объект **PSCredential** можно настроить так, чтобы участие пользователя не требовалось.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="e9c0f-119">Сначала необходимо задать надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="e9c0f-120">Для начала нужно придумать текстовый пароль и преобразовать его в защищенную строку с помощью командлета [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="e9c0f-121">Далее следует преобразовать защищенную строку в зашифрованную стандартную строку, используя командлет [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="e9c0f-122">После этого вы можете сохранить зашифрованную стандартную строку в файл с помощью командлета [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="e9c0f-123">Можно также создать файл с надежным паролем, чтобы не нужно было каждый раз вводить пароль.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="e9c0f-124">Кроме того, файл с надежным паролем безопаснее, чем обычный текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="e9c0f-125">Для создания файла надежного пароля используйте эту команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e9c0f-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="e9c0f-126">При выборе пароля убедитесь, что соблюдены [требования к сложности](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="e9c0f-127">Чтобы создать объект учетных данных из файла с надежным паролем, необходимо считать содержимое файла и преобразовать его обратно в защищенную строку с помощью командлета [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c0f-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="e9c0f-128">Командлет [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) принимает также параметр *Expiration* , который указывает значение **DateTime** , определяющее дату и время истечения срока действия учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="e9c0f-129">Например, можно задать срок действия учетной записи, который истечет через несколько дней.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="e9c0f-130">В этом примере показано, как установить расширение удаленного рабочего стола для облачной службы с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e9c0f-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="e9c0f-131">При необходимости вы также можете указать слот развертывания и роли, для которых необходимо включить удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="e9c0f-132">Если эти параметры не указаны, командлет по умолчанию включит использование удаленного рабочего стола для всех ролей в слоте развертывания **рабочей среды** .</span><span class="sxs-lookup"><span data-stu-id="e9c0f-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="e9c0f-133">Расширение удаленного рабочего стола привязывается к развернутой службе.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="e9c0f-134">В случае создания нового развертывания службы потребуется включить использование удаленного рабочего стола для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="e9c0f-135">Если необходимо, чтобы использование удаленного рабочего стола включалось всегда, рассмотрите возможность интеграции соответствующих сценариев PowerShell в рабочий процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="e9c0f-136">Подключение к экземпляру роли по протоколу удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="e9c0f-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="e9c0f-137">Командлет [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) можно использовать, чтобы добавить удаленный рабочий стол для определенного экземпляра роли облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="e9c0f-138">Можно использовать параметр *LocalPath* , чтобы скачать RDP-файл на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="e9c0f-139">Вы можете также использовать параметр *Launch* , чтобы открыть диалоговое окно "Подключение к удаленному рабочему столу" для доступа к экземпляру роли облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="e9c0f-140">Убедитесь, что расширение удаленного рабочего стола включено в службе.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="e9c0f-141">Командлет [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) показывает, включен ли удаленный рабочий стол в развернутой службе.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="e9c0f-142">Он возвращает имя пользователя удаленного рабочего стола и роли, для которых включено расширение удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="e9c0f-143">По умолчанию это выполняется в слоте развертывания, и вы можете выбрать слот промежуточного развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="e9c0f-144">Удаление расширения удаленного рабочего стола из службы</span><span class="sxs-lookup"><span data-stu-id="e9c0f-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="e9c0f-145">Если вы уже включили расширение удаленного рабочего стола в развернутой службе и хотите обновить параметры удаленного рабочего стола, то сначала удалите расширение удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="e9c0f-146">Затем снова включите его с новыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-146">And enable it again with the new settings.</span></span> <span data-ttu-id="e9c0f-147">Например, если вы хотите задать новый пароль для учетной записи удаленного пользователя или ее срок действия истек.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="e9c0f-148">Данное действие необходимо только для существующих развертываний, в которых включено расширение удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="e9c0f-149">К новым развертываниям можно непосредственно применить расширение.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="e9c0f-150">Чтобы удалить расширение удаленного рабочего стола из развернутой службы, используйте командлет [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="e9c0f-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="e9c0f-151">При необходимости можно также указать слот развертывания и роль, для которой необходимо удалить удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="e9c0f-152">Чтобы полностью удалить конфигурацию расширения, выполните командлет *remove* с параметром **UninstallConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="e9c0f-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="e9c0f-153">Параметр **UninstallConfiguration** удаляет все конфигурации расширения, примененные к службе.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="e9c0f-154">Каждая конфигурация расширения связана с конфигурацией службы.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="e9c0f-155">Вызов командлета *remove* без параметра **UninstallConfiguration** разорвет связь <mark>развертывания</mark> с конфигурацией расширения, фактически удаляя это расширение.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="e9c0f-156">Однако конфигурация расширения будет по-прежнему связана со службой.</span><span class="sxs-lookup"><span data-stu-id="e9c0f-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="e9c0f-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e9c0f-157">Additional resources</span></span>

<span data-ttu-id="e9c0f-158">[Настройка облачных служб](cloud-services-how-to-configure.md)
[Часто задаваемые вопросы об облачных службах](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e9c0f-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
