---
title: "Развертывание шаблонов с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Дополнительные сведения о развертывании виртуальной машины с помощью шаблона диспетчера ресурсов и PowerShell."
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
ms.openlocfilehash: 1f443898bcb9b422fc2db46f4e389ae51b043d87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>Развертывание шаблонов в Azure Stack с помощью PowerShell
Использование PowerShell для развертывания пакета средств разработки Azure стека шаблонов диспетчера ресурсов Azure.  Шаблоны диспетчера ресурсов, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.

## <a name="run-azurerm-powershell-cmdlets"></a>Выполнение командлетов PowerShell для AzureRM
В этом примере выполнить сценарий для развертывания виртуальной машины в комплекте разработки Azure стека с помощью шаблона диспетчера ресурсов.  Прежде чем продолжить, убедитесь в наличии [настроить PowerShell](azure-stack-powershell-configure-user.md)  

Виртуальный жесткий ДИСК, используемый в данном примере шаблоне — WindowsServer 2012-R2 Datacenter.

1. Последовательно выберите пункты <http://aka.ms/AzureStackGitHub>, поиск **101-simple-windows-vm** шаблона и сохраните его в следующее расположение: c:\\шаблоны\\ azuredeploy-101-simple-windows-vm.json.
2. В PowerShell выполните следующий сценарий развертывания. Замените *username* и *пароль* имя пользователя и пароль. При последующем использовании увеличить значение для *$myNum* параметр для предотвращения перезаписи развертывания.
   
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
3. Открыть портала, нажмите кнопку Azure стека **Обзор**, нажмите кнопку **виртуальные машины**и найдите на новую виртуальную машину (*myDeployment001*).


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание шаблонов с помощью Visual Studio](azure-stack-deploy-template-visual-studio.md)

