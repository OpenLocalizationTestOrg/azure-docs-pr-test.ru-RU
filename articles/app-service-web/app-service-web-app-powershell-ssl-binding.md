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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Привязка SSL-сертификатов службы приложений Azure с помощью PowerShell
С выпуском Microsoft Azure PowerShell версии 1.1.0, добавлен новый командлет hello, будет получен hello пользователя hello возможность toobind существующего или нового SSL сертификаты tooan существующее веб-приложение.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn об использовании диспетчера ресурсов Azure на основе toomanage командлеты Azure PowerShell возврат веб-приложений [диспетчера ресурсов Azure на основе команд PowerShell для веб-приложения Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Передача и привязка нового SSL-сертификата
Сценарий: hello пользователь предпочитает toobind tooone сертификат SSL, его веб-приложений.

Имя группы ресурсов hello, содержащий hello веб-приложения, имя веб-приложения hello, hello путь к файлу сертификата PFX-файл на компьютере пользователя hello hello пароль для сертификата hello и hello пользовательское имя узла, мы можем hello, следуя toocreate команду PowerShell, Привязка SSL.

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Обратите внимание, что перед добавлением веб-приложении tooa привязки SSL, необходимо иметь имя узла (пользовательский домен) уже настроен. Если имя узла hello не настроен, то вы получите ошибку при выполнении New AzureRmWebAppSSLBinding «hostname» не существует. Имя узла можно добавлять непосредственно из портала hello или с помощью Azure PowerShell. Hello следующий фрагмент команды PowerShell может быть имя узла hello tooconfigure перед запуском создать AzureRmWebAppSSLBinding.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Очень важно, hello командлет Set-AzureRmWebApp toounderstand перезаписи hello имена узлов для веб-приложения hello. Поэтому hello выше фрагмент команды PowerShell добавления существующего списка toohello приветствия имен узлов для веб-приложения hello.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Передача и привязка существующего SSL-сертификата
Сценарий: hello пользователь предпочитает toobind ранее отправленные tooone сертификат SSL, его веб-приложений.

Мы можем получить список сертификатов hello уже отправленного tooa определенной группы ресурсов, используя следующую команду hello

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Обратите внимание, что hello сертификаты — локальный tooa конкретного расположения и группе ресурсов hello пользователю необходимо toore — отправка сертификата hello Если hello настроить веб-приложение находится в другом месте и групп ресурсов, другие, который hello требуется сертификат 

Зная hello имя группы ресурсов, содержащий веб-приложения hello, имя веб-приложения hello, hello отпечаток сертификата и hello пользовательское имя узла, hello, следующая команда toocreate PowerShell можно использовать эту привязку SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Удаление существующей привязки SSL-подключения
Сценарий: hello пользователь предпочитает toodelete существующую привязку SSL.

Имя группы ресурсов hello, который содержит веб-приложения hello, зная hello имя веб-приложения и hello пользовательское имя узла, hello, следующая команда tooremove PowerShell можно использовать эту привязку SSL:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Обратите внимание, что если hello удалить привязку SSL был hello последнего привязки с помощью этого сертификата в этом расположении сертификатом по умолчанию hello будут удалены, пользователь hello tookeep hello сертификата он можно воспользоваться hello DeleteCertificate параметр tookeep hello сертификата

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Ссылки
* [Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Введение tooApp среды службы](app-service-app-service-environment-intro.md)
* [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md)

