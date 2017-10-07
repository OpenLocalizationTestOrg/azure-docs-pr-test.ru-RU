---
title: "шаблоны aaaDeploy с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальной машины с помощью шаблона диспетчера ресурсов и PowerShell."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: fb0d4b190e058b3c5c1273b6c91fc3d72dedeb1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>Развертывание шаблонов в Azure Stack с помощью PowerShell
С помощью PowerShell toodeploy диспетчера ресурсов Azure шаблоны toohello пакет средств разработки Azure стека.  Шаблоны диспетчера ресурсов, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.

## <a name="run-azurerm-powershell-cmdlets"></a>Выполнение командлетов PowerShell для AzureRM
В этом примере выполняется toodeploy сценарий виртуальной машины tooAzure стека пакет средств разработки с помощью шаблона диспетчера ресурсов.  Прежде чем продолжить, убедитесь в наличии [настроить PowerShell](azure-stack-powershell-configure-user.md)  

Hello VHD, используемые в данном примере шаблоне — WindowsServer 2012-R2 Datacenter.

1. Go слишком<http://aka.ms/AzureStackGitHub>, поиск hello **101-simple-windows-vm** шаблона и сохраните его toohello следующие расположения: c:\\шаблоны\\ azuredeploy-101-simple-windows-vm.json.
2. В PowerShell запустите следующий скрипт развертывания hello. Замените *username* и *пароль* имя пользователя и пароль. При последующем использовании увеличивать значение hello для hello *$myNum* tooprevent параметр перезаписи развертывания.
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. Откройте hello Azure стека, щелкните **Обзор**, нажмите кнопку **виртуальные машины**и найдите на новую виртуальную машину (*myDeployment001*).


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание шаблонов с помощью Visual Studio](azure-stack-deploy-template-visual-studio.md)

