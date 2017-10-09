---
title: "Сертификаты aaaSSL привязки с помощью PowerShell"
description: "Узнайте, как toobind SSL-сертификатов tooyour веб-приложения с помощью PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="29585-103">Привязка SSL-сертификатов службы приложений Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="29585-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="29585-104">С выпуском Microsoft Azure PowerShell версии 1.1.0, добавлен новый командлет hello, будет получен hello пользователя hello возможность toobind существующего или нового SSL сертификаты tooan существующее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="29585-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="29585-105">toolearn об использовании диспетчера ресурсов Azure на основе toomanage командлеты Azure PowerShell возврат веб-приложений [диспетчера ресурсов Azure на основе команд PowerShell для веб-приложения Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="29585-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="29585-106">Передача и привязка нового SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="29585-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="29585-107">Сценарий: hello пользователь предпочитает toobind tooone сертификат SSL, его веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="29585-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="29585-108">Имя группы ресурсов hello, содержащий hello веб-приложения, имя веб-приложения hello, hello путь к файлу сертификата PFX-файл на компьютере пользователя hello hello пароль для сертификата hello и hello пользовательское имя узла, мы можем hello, следуя toocreate команду PowerShell, Привязка SSL.</span><span class="sxs-lookup"><span data-stu-id="29585-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="29585-109">Обратите внимание, что перед добавлением веб-приложении tooa привязки SSL, необходимо иметь имя узла (пользовательский домен) уже настроен.</span><span class="sxs-lookup"><span data-stu-id="29585-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="29585-110">Если имя узла hello не настроен, то вы получите ошибку при выполнении New AzureRmWebAppSSLBinding «hostname» не существует.</span><span class="sxs-lookup"><span data-stu-id="29585-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="29585-111">Имя узла можно добавлять непосредственно из портала hello или с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29585-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="29585-112">Hello следующий фрагмент команды PowerShell может быть имя узла hello tooconfigure перед запуском создать AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="29585-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="29585-113">Очень важно, hello командлет Set-AzureRmWebApp toounderstand перезаписи hello имена узлов для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="29585-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="29585-114">Поэтому hello выше фрагмент команды PowerShell добавления существующего списка toohello приветствия имен узлов для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="29585-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="29585-115">Передача и привязка существующего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="29585-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="29585-116">Сценарий: hello пользователь предпочитает toobind ранее отправленные tooone сертификат SSL, его веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="29585-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="29585-117">Мы можем получить список сертификатов hello уже отправленного tooa определенной группы ресурсов, используя следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="29585-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="29585-118">Обратите внимание, что hello сертификаты — локальный tooa конкретного расположения и группе ресурсов hello пользователю необходимо toore — отправка сертификата hello Если hello настроить веб-приложение находится в другом месте и групп ресурсов, другие, который hello требуется сертификат</span><span class="sxs-lookup"><span data-stu-id="29585-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="29585-119">Зная hello имя группы ресурсов, содержащий веб-приложения hello, имя веб-приложения hello, hello отпечаток сертификата и hello пользовательское имя узла, hello, следующая команда toocreate PowerShell можно использовать эту привязку SSL:</span><span class="sxs-lookup"><span data-stu-id="29585-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="29585-120">Удаление существующей привязки SSL-подключения</span><span class="sxs-lookup"><span data-stu-id="29585-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="29585-121">Сценарий: hello пользователь предпочитает toodelete существующую привязку SSL.</span><span class="sxs-lookup"><span data-stu-id="29585-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="29585-122">Имя группы ресурсов hello, который содержит веб-приложения hello, зная hello имя веб-приложения и hello пользовательское имя узла, hello, следующая команда tooremove PowerShell можно использовать эту привязку SSL:</span><span class="sxs-lookup"><span data-stu-id="29585-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="29585-123">Обратите внимание, что если hello удалить привязку SSL был hello последнего привязки с помощью этого сертификата в этом расположении сертификатом по умолчанию hello будут удалены, пользователь hello tookeep hello сертификата он можно воспользоваться hello DeleteCertificate параметр tookeep hello сертификата</span><span class="sxs-lookup"><span data-stu-id="29585-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="29585-124">Ссылки</span><span class="sxs-lookup"><span data-stu-id="29585-124">References</span></span>
* [<span data-ttu-id="29585-125">Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="29585-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="29585-126">Введение tooApp среды службы</span><span class="sxs-lookup"><span data-stu-id="29585-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="29585-127">Использование Azure PowerShell с диспетчером ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="29585-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

