---
title: "hello aaaUse модуля политики стек Azure | Документы Microsoft"
description: "Узнайте, как подписка Azure стека tooconstrain toobehave подписки Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a>Управление Azure политикой, с помощью hello модуля политики стек Azure
модуль политики стек Azure Hello позволяет tooconfigure подписку Azure с hello же управления версиями и доступность службы как стек Azure.  модуль Hello использует hello **New AzureRMPolicyAssignment** toocreate командлет политику Azure, которая ограничивает типы ресурсов hello и служб, доступных по подписке.  После завершения можно использовать приложения toodevelop подписки Azure для Azure стека.  

## <a name="install-hello-module"></a>Установка модуля hello
1. Установите необходимую версию hello hello модуль AzureRM PowerShell, как описано в шаг 1 из [Установка PowerShell для Azure стека](azure-stack-powershell-install.md).   
2. [Загрузить набор средств Azure стека hello из GitHub](azure-stack-powershell-download.md)  
3. [Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md) (Настройка PowerShell для использования с Azure Stack)

4. Импорт модуля AzureStack.Policy.psm1 hello:

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a>Применить политику toosubscription
Hello следующую команду можно использовать tooapply политику по умолчанию стек Azure к подписке Azure. Перед запуском, замените *имя подписки Azure* с подпиской Azure.

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a>Группа ресурсов tooa политики применения
Вы можете tooapply политик в более детального метод.  Например, возможно, других ресурсов, выполняемых в hello одной подписке.  Вы можете задать область hello политики приложения tooa определенной группы ресурсов, используемое для тестирования приложений для Azure стека с помощью ресурсов Azure. Перед запуском, замените *имя подписки Azure* именем своей подписке Azure.

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a>Политика в действии
После развертывания hello Azure политики, возникает ошибка при попытке toodeploy ресурс, который запрещено политикой.  

![Результат сбоя развертывания ресурсов из-за ограничений политики](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)

[Развертывание шаблонов с помощью интерфейса командной строки Azure](azure-stack-deploy-template-command-line.md)

[Развертывание шаблонов с помощью Visual Studio](azure-stack-deploy-template-visual-studio.md)
