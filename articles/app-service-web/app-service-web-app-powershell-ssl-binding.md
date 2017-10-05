---
title: "Привязка SSL-сертификатов с помощью PowerShell"
description: "Узнайте, как привязать SSL-сертификаты к веб-приложению с помощью PowerShell."
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="299a8-103">Привязка SSL-сертификатов службы приложений Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="299a8-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="299a8-104">В выпуске Microsoft Azure PowerShell версии 1.1.0 был добавлен новый командлет, позволяющий привязывать существующие или новые SSL-сертификаты к существующему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="299a8-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="299a8-105">Дополнительные сведения об использовании командлетов Azure PowerShell на основе Azure Resource Manager для управления веб-приложениями см. [здесь](app-service-web-app-azure-resource-manager-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="299a8-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="299a8-106">Передача и привязка нового SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="299a8-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="299a8-107">Сценарий: пользователь хочет привязать SSL-сертификат к одному из своих веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="299a8-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="299a8-108">Зная имя группы ресурсов, в которую входит веб-приложение, имя веб-приложения, путь к PFX-файлу сертификата на компьютере пользователя, пароль к сертификату и пользовательское имя узла, можно создать привязку SSL-подключения с помощью следующей команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="299a8-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="299a8-109">Обратите внимание, что перед добавлением привязки SSL для веб-приложения необходимо настроить имя узла (пользовательский домен).</span><span class="sxs-lookup"><span data-stu-id="299a8-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="299a8-110">Если имя узла не настроено, то при запуске командлета New-AzureRmWebAppSSLBinding будет выдана ошибка "Имя узла не существует".</span><span class="sxs-lookup"><span data-stu-id="299a8-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="299a8-111">Имя узла можно добавить непосредственно с портала или с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="299a8-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="299a8-112">Настроить имя узла перед запуском командлета New-AzureRmWebAppSSLBinding можно с помощью следующего фрагмента PowerShell.</span><span class="sxs-lookup"><span data-stu-id="299a8-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="299a8-113">Важно понимать, что командлет Set-AzureRmWebApp перезаписывает имена узлов для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="299a8-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="299a8-114">Таким образом, в приведенном выше фрагменте PowerShell производится добавление имен узлов для веб-приложения в существующий список.</span><span class="sxs-lookup"><span data-stu-id="299a8-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="299a8-115">Передача и привязка существующего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="299a8-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="299a8-116">Сценарий: пользователь хочет привязать загруженный ранее SSL-сертификат к одному из своих веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="299a8-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="299a8-117">Получить список сертификатов, уже загруженных в определенную группу ресурсов, можно с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="299a8-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="299a8-118">Обратите внимание, что сертификаты являются локальными и относятся в определенному расположению и группе ресурсов, так что в случае, если выбранное веб-приложение и необходимый сертификат находятся в разных расположениях и группах ресурсов, сертификат необходимо передать заново.</span><span class="sxs-lookup"><span data-stu-id="299a8-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="299a8-119">Зная имя группы ресурсов, в которую входит веб-приложение, имя веб-приложения, отпечаток сертификата и пользовательское имя узла, можно создать привязку SSL-подключения с помощью следующей команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="299a8-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="299a8-120">Удаление существующей привязки SSL-подключения</span><span class="sxs-lookup"><span data-stu-id="299a8-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="299a8-121">Сценарий: пользователь хочет удалить существующую привязку SSL-подключения.</span><span class="sxs-lookup"><span data-stu-id="299a8-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="299a8-122">Зная имя группы ресурсов, в которую входит веб-приложение, имя веб-приложения и пользовательское имя узла, можно удалить соответствующую привязку SSL-подключения с помощью следующей команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="299a8-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="299a8-123">Обратите внимание: если удаляемая привязка SSL-подключения является последней привязкой, использующей сертификат в указанном расположении, по умолчанию этот сертификат удаляется; для сохранения сертификата используйте параметр DeleteCertificate.</span><span class="sxs-lookup"><span data-stu-id="299a8-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="299a8-124">Ссылки</span><span class="sxs-lookup"><span data-stu-id="299a8-124">References</span></span>
* [<span data-ttu-id="299a8-125">Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="299a8-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="299a8-126">Введение в среду службы приложения</span><span class="sxs-lookup"><span data-stu-id="299a8-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="299a8-127">Использование Azure PowerShell с диспетчером ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="299a8-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

